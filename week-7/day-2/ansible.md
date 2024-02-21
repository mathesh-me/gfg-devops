### Continuation of Ansible Day-1

**Now we deployed a Load Balancer and 2 Web Servers. The problem we have is we manually need to update the Load Balancer IP in the /etc/haproxy/haproxy.cfg file.**

### Dynamic IP updation in /etc/haproxy/haproxy.cfg file

- We are going to update the load-balancer.yml file to dyanamically update the IP of the web servers in the haproxy.cfg file.
```yaml
- hosts: localhost
  vars_files:
    - credentials.yml
    - ec2-config.yml
  tasks:
    - package:
        name: haproxy
        state: present

    - amazon.aws.ec2_instance_info:
        aws_access_key: "{{ access_key }}"
        aws_secret_key: "{{ secret_access_key }}"
        region: "{{ region }}"
        filters:
          "tag:Name": "ansible-demo"
          instance-state-name: ["running"]
      register: ec2

    - set_fact:
        private_ip: "{{ ec2.instances | map(attribute='private_ip_address') | list }}"

    - debug:
        var: private_ip

    - template:
        src: haproxy.j2
        dest: /etc/haproxy/haproxy.cfg

    - service:
        name: haproxy
        state: restarted
```

- What we done here is we are going to get the isntances that is created by our ec2.yml playbook and then we are going to get the private IP of the instances and then we are going to update the haproxy.cfg file with the private IP of the instances.
- **aws.ec2_instance_info** is a module that is used to get the information of the instances that is created by the ec2.yml playbook.
- **register** is a keyword that is used to store the output of the module in a variable. In our case `ec2` variable.
- **set_fact** is a module that is used to set the value of a private_ip variable.
- **template** is a module that is used to update the haproxy.cfg file with the private IP of the instances.
- **debug** is a module that is used to print the value of the private_ip variable.

- You can see that in `load-balancer.yml` file, We used to use `template` module to update the haproxy.cfg file. But we need to create a template file to update the haproxy.cfg file. So we need to create a template file called `haproxy.j2` in the same directory where the `load-balancer.yml` file is present.
- Let's create a `haproxy.j2` file.
```yaml
#---------------------------------------------------------------------
# Example configuration for a possible web application.  See the
# full configuration options online.
#
#   https://www.haproxy.org/download/1.8/doc/configuration.txt
#
#---------------------------------------------------------------------

#---------------------------------------------------------------------
# Global settings
#---------------------------------------------------------------------
global
    # to have these messages end up in /var/log/haproxy.log you will
    # need to:
    #
    # 1) configure syslog to accept network log events.  This is done
    #    by adding the '-r' option to the SYSLOGD_OPTIONS in
    #    /etc/sysconfig/syslog
    #
    # 2) configure local2 events to go to the /var/log/haproxy.log
    #   file. A line like the following can be added to
    #   /etc/sysconfig/syslog
    #
    #    local2.*                       /var/log/haproxy.log
    #
    log         127.0.0.1 local2

    chroot      /var/lib/haproxy
    pidfile     /var/run/haproxy.pid
    maxconn     4000
    user        haproxy
    group       haproxy
    daemon

    # turn on stats unix socket
    stats socket /var/lib/haproxy/stats

    # utilize system-wide crypto-policies
    ssl-default-bind-ciphers PROFILE=SYSTEM
    ssl-default-server-ciphers PROFILE=SYSTEM

#---------------------------------------------------------------------
# common defaults that all the 'listen' and 'backend' sections will
# use if not designated in their block
#---------------------------------------------------------------------
defaults
    mode                    http
    log                     global
    option                  httplog
    option                  dontlognull
    option http-server-close
    option forwardfor       except 127.0.0.0/8
    option                  redispatch
    retries                 3
    timeout http-request    10s
    timeout queue           1m
    timeout connect         10s
    timeout client          1m
    timeout server          1m
    timeout http-keep-alive 10s
    timeout check           10s
    maxconn                 3000

#---------------------------------------------------------------------
# main frontend which proxys to the backends
#---------------------------------------------------------------------
frontend main
    bind *:5000
    acl url_static       path_beg       -i /static /images /javascript /stylesheets
    acl url_static       path_end       -i .jpg .gif .png .css .js

    use_backend static          if url_static
    default_backend             app

#---------------------------------------------------------------------
# static backend for serving up images, stylesheets and such
#---------------------------------------------------------------------
backend static
    balance     roundrobin
    server      static 127.0.0.1:4331 check

#---------------------------------------------------------------------
# round robin balancing between the various backends
#---------------------------------------------------------------------
backend app
    balance     roundrobin
  {% for ip in private_ip %}
  server app{{ ip.split('.')[-1] }} {{ ip }}:80 check
  {% endfor %}
```

- In the above file we used jinja for loop to update the private IP of the instances in the haproxy.cfg file.

- Now we need to run the `load-balancer.yml` file to update the haproxy.cfg file.
```bash
ansible-playbook load-balancer.yml
```
- After running the above command, you can see that the haproxy.cfg file is updated with the private IP of the instances.

### Get IP address of our server in our Page:

- We can use the backend service of our httpd server to get the IP of the server in our page.
- For this purpose, We are going to use python subproccess module to get the IP of the server and then we are going to use the IP in our page.
- Let's create `python_cgi_ip.py` file
```
#!/usr/bin/env python3

import subprocess

print("Content-type: text/html\n")  # CGI header

print("<html>")
print("<head><title>CGI ifconfig</title></head>")
print("<body>")

ifconfig_output = subprocess.getoutput("ifconfig")
print("<pre>{}</pre>".format(ifconfig_output))
print("</body>")
print("</html>")
```

- We are going to copy this file to our httpd server and then we are going to use the backend service to get the IP of the server in our page.
- This step also we are going to automate using ansible.
- Let's update the `httpd.yml` file to copy the `python_cgi_ip.py` file to the httpd server.
```yaml
- hosts: all
  tasks:

    - name: Installing the HTTPD Package
      package:
        name: httpd
        state: present

    - name: Copying Files from Localhost to Remote
      copy:
        src: index.html
        dest: /var/www/html
        owner: root
        mode: '666'

    - name: "copy the cgi program"
      copy:
        src: python_cgi_ip.py
        dest: /var/www/cgi-bin/ip.py

    - command: "chmod +x /var/www/cgi-bin/ip.py"

    - name: Starting the Service
      service:
        name: httpd
        state: started
```

- In the above `httpd.yml` file, We added a new task to copy the `python_cgi_ip.py` file to the httpd server.
- And we also added a new task to change the permission of the `python_cgi_ip.py` file to executable.
- Now, Let's run the `httpd.yml` file to copy the `python_cgi_ip.py` file to the httpd server.
```bash
ansible-playbook httpd.yml
```
- Now we can the load balancer IP in the browser to see the IP of the server.

### Ansible roles

- Roles let you automatically load related vars, files, tasks, handlers, and other Ansible artifacts based on a known file structure. After you group your content into roles, you can easily reuse them and share them with other users.
- Run `ansible-galaxy init role-name` to create a new role.
- After running the above command, You can see that a new directory called `role-name` is created with the following structure.
```
role-name
├── defaults
│   └── main.yml
├── files
├── handlers
│   └── main.yml
├── meta
│   └── main.yml
├── README.md
├── tasks
│   └── main.yml
├── templates
├── tests
│   ├── inventory
│   └── test.yml
└── vars
    └── main.yml
```
- We just need the arrange the files in the above structure and then we can use the role in our playbook.

### Ansible Vault

- Ansible Vault is a feature of ansible that allows you to keep sensitive data such as passwords or keys in encrypted files, rather than as plaintext in your playbooks or roles.
- You can use ansible-vault to encrypt the file and then you can use the file in your playbook.
- Run `ansible-vault create file-name` to create a new encrypted file. It will ask for a password to encrypt the file.
- You can also put that password in another file and use that file to encrypt the file.
- Run `ansible-vault create file_name --vault-password-file file_name_where_your_passwdIsStored` to encrypt the file.
- If we used any encrypted file in our playbook, We need to use `ansible-playbook --vault-password-file playbook.yml` to run the playbook.

- **Note**: You can also use `ansible-vault edit file_name` to edit the encrypted file.
