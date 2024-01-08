## Linux

### What is Linux OS?

- Linux is a open source operating system. It is a free operating system. It provides better Security, flexibility, stability, etc. It is used in servers, desktops, mobiles, etc.
- It Provides better Customization Support over Windows, Mac.
- There are various Linux Distribution like RedHat, Ubuntu, CentOS, etc. Each Linux Distribution has its own features and functionalities.
- In Linux, We can have command line interface and graphical user interface. We can use any one of them based on our requirement.
- In Linux, We can use command line interface to perform various operations.

### Basic Linux Commands

- **pwd** - It is used to print the current working directory.
- **ls** - It is used to list the files and directories in the current working directory.
- **cd** - It is used to change the directory.
- **mkdir** - It is used to create a directory.
- **touch** - It is used to create a file.
- **cat** - It is used to print the content of the file.
- **id** - It is used to print the user id and group id.

### Linux File System

- In Linux, We have a root director (/). All the files and directories are stored in the root directory.

### How to install Linux OS(any distribution)?

1. Bare Metal - Install Linux OS directly on the hardware.
2. Virtualization - Install Linux OS on the virtual machine. There are various virtualization tools like VirtualBox, Hyper-V, etc.
3. Cloud - Install Linux OS on the cloud. There are various cloud providers like AWS, Azure, GCP, etc.
4. Container - Install Linux OS on the container. There are various containerization tools like Docker, Kubernetes, etc.


### Hosting Apache Web Server on Linux OS

- Use the below command to install apache web server on Linux OS:
```
sudo yum install -y apache2
```

- Use the below Command to edit the index.html file:
```
sudo nano /var/www/html/index.html
```

- Use the below command to start the apache web server:
```
sudo systemctl start apache2
```

- Use the below command to stop the apache web server:
```
sudo systemctl stop apache2
```

### vi editor

- Use the below command to edit the file using vi editor:
```
vi <file-name>
```

- Use the below command to insert the text in the file:
```
i
```

- Use the below command to save the file:
```
:wq
```

- Use the below command to exit from the file without saving the file:
```
:q!
```