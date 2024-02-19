## Ansible

### Why Ansible?

- Let's say we have 100 of servers and we want to install a package on all of them. We can do it manually by ssh into each server and install the package. But it will take a lot of time and effort. Instead of doing it manually, we can use the automation tools like Ansible.

### What is Ansible?

- Ansible is an open-source automation tool that automates the software provisioning, configuration management, and application deployment.

- Advantages of Ansible:
    - **Declerative**: We can define the state of the system and Ansible will make sure that the system is in that state.
    - **Agentless**: We don't have to install any agent on the remote servers.
    - **Idempotent**: We can run the playbook multiple times and it will not change the state of the system if it is already in that state.

- Ansible is written in Python and it uses the YAML syntax to write the playbooks.

### Command to install Ansible on Amazon Linux 3

```bash
yum install ansible-core -y
```

### Ansible configuration file

- The default configuration file for Ansible is `/etc/ansible/ansible.cfg`.


### Inventory file in Ansible

- Inventory file is used to define the list of servers on which we want to run the playbooks.




