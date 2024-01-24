## Docker Commands, Features, and Use Cases

**Continuation from week 2 day 2**

### Docker Commands

- **docker inspect <container_name>** - This command will allow you to inspect a container. It will give you detailed information about the container such as the IP address, the volumes, the environment variables, etc.
- **docker exec -it <container_name> bash** - This command will allow you to enter a running container and run commands inside of it with the help of bash program.
- **docker run -it -p 80:80 -v /local_dir:/container_dir <image_name>** - This command will allow you to run a container with the help of an image. The -it flag will allow you to run the container in interactive mode. The -p flag will allow you to map the port of the container to the port of the host machine. The -v flag will allow you to map a local directory to a directory inside of the container. This is useful for mounting volumes. So we can have a persistent storage for our containers.
- **docker cp <container_name>:<container_dir> <local_dir>** - This command will allow you to copy files from a container to your local machine.
- **docker cp <local_dir> <container_name>:<container_dir>** - This command will allow you to copy files from your local machine to a container.

### Dockerfile

It is a file that contains instructions on how to build an image. It is a text file that contains a list of commands that the docker client calls while creating an image. It is a simple way to automate the image creation process. The best part is that the commands you write in a Dockerfile are almost identical to their equivalent Linux commands. This means you don’t really have to learn new syntax to create your own dockerfiles.

**Example Dockerfile**

```dockerfile
FROM ubuntu:latest
RUN apt-get update
RUN apt-get install -y nginx
CMD ["nginx", "-g", "daemon off;"]
```

After creating a Dockerfile, you can build an image with the help of the following command:

```bash
docker build -t <image_name> .
```

**Dockerfile Instructions**

- **FROM** - This instruction is used to specify the base image. You can specify any image of your choice as the base image. The image can be from your local machine or from a remote repository like Docker Hub.
- **RUN** - This instruction is used to run commands inside of the container. You can run any command that you would normally run on a Linux machine.
- **LABEL** - This instruction is used to add metadata to the image. You can specify any key-value pair as metadata such as maintainer, description, version, etc.
- **COPY** - This instruction is used to copy files from the local machine to the container.
- **ENV** - This instruction is used to set environment variables inside of the container.
- **WORKDIR** - This instruction is used to set the working directory for the instructions that follow it.
- **CMD** - This instruction is used to specify the command that needs to be executed when a container is created from the image. You can specify any command that you would normally run on a Linux machine.
- **ENTRYPOINT** - This instruction is used to specify the command that needs to be executed when a container is created from the image. You can specify any command that you would normally run on a Linux machine. The difference between CMD and ENTRYPOINT is that CMD can be overridden by passing arguments to the docker run command. Whereas, ENTRYPOINT cannot be overridden by passing arguments to the docker run command.

- **CMD** vs **ENTRYPOINT** - The difference between CMD and ENTRYPOINT is that CMD can be overridden by passing arguments to the docker run command. Whereas, ENTRYPOINT cannot be overridden by passing arguments to the docker run command. For example, if you have a Dockerfile with the following CMD instruction:

```dockerfile
CMD ["nginx", "-g", "daemon off;"]
```

You can override the CMD instruction by passing arguments to the docker run command like this:

```bash
docker run -it <image_name> bash
```

But if you have a Dockerfile with the following ENTRYPOINT instruction:

```dockerfile
ENTRYPOINT ["nginx", "-g", "daemon off;"]
```

You cannot override the ENTRYPOINT instruction by passing arguments to the docker run command like this:

```bash
docker run -it <image_name> bash
```

### Docker Compose

It is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application’s services. Then, with a single command, you create and start all the services from your configuration.

**Example docker-compose.yml**

```yaml
version: '3.1'

services:

  wordpress:
    image: wordpress
    restart: always
    ports:
      - 8080:80
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: exampleuser
      WORDPRESS_DB_PASSWORD: examplepass
      WORDPRESS_DB_NAME: exampledb
    volumes:
      - wordpress:/var/www/html

  db:
    image: mysql:8.0
    restart: always
    environment:
      MYSQL_DATABASE: exampledb
      MYSQL_USER: exampleuser
      MYSQL_PASSWORD: examplepass
      MYSQL_RANDOM_ROOT_PASSWORD: '1'
    volumes:
      - db:/var/lib/mysql

volumes:
  wordpress:
  db:
```

After creating a docker-compose.yml file, you can run the following command to start the application:

```bash
docker-compose up -d
```
To delete all the containers created by docker-compose, you can run the following command:

```bash
docker-compose down
```

### Docker Hub

It is a cloud-based registry service which allows you to link to code repositories, build your images and test them, stores manually pushed images, and links to Docker Cloud so you can deploy images to your hosts. It provides a centralized resource for container image discovery, distribution and change management, user and team collaboration, and workflow automation throughout the development pipeline.

To push an image to Docker Hub, you can run the following commands:

```bash
docker login
docker tag <image_name> <docker_hub_username>/<image_name>
docker push <docker_hub_username>/<image_name>
```

To pull an image from Docker Hub, you can run the following command:

```bash
docker pull <docker_hub_username>/<image_name>
```

To Push image into any other registry, you can run the following commands:

```bash
docker login <registry_url>
docker tag <image_name> <registry_url>/<image_name>
docker push <registry_url>/<image_name>
```

## Docker Networking

- **docker network ls** - This command will allow you to list all the networks.
- **docker network create <network_name>** - This command will allow you to create a network.
- **docker network inspect <network_name>** - This command will allow you to inspect a network. It will give you detailed information about the network such as the IP address, the containers connected to the network, etc.
- **docker network connect <network_name> <container_name>** - This command will allow you to connect a container to a network.
- **docker network disconnect <network_name> <container_name>** - This command will allow you to disconnect a container from a network.

How Docker Networking Works

- **SDN** - Docker uses SDN (Software Defined Networking) to create and manage networks. It creates a virtual network bridge on the host machine. This bridge is used to connect the containers to the network.

---


There are four types of networks in Docker:

- **Bridge** - This is the default network type. It provides communication between the host and the containers. It also provides communication between the containers on the same host.
- **Host** - This network type removes the network isolation between the host and the containers. It also removes the network isolation between the containers on the same host.
- **None** - This network type removes the network isolation between the containers on the same host. But it does not provide communication between the host and the containers.
- **Overlay** - This network type provides communication between the containers running on different hosts.

You can refer Docker Networking documentation for more information.
You can attach a container to a network while creating it with the help of the following command:

```bash
docker run -it --network <network_name> <image_name>
```

## Docker Volumes

- **docker volume ls** - This command will allow you to list all the volumes.
- **docker volume create <volume_name>** - This command will allow you to create a volume.
- **docker volume inspect <volume_name>** - This command will allow you to inspect a volume. It will give you detailed information about the volume such as the mount point, the containers connected to the volume, etc.

### Docker Limits

- **docker run -it --memory <memory_limit> <image_name>** - This command will allow you to limit the memory usage of a container.
- **docker run -it --cpus <cpu_limit> <image_name>** - This command will allow you to limit the CPU usage of a container.

### Other Commands, Information, and Files

- **ps aux** - This command will allow you to list all the running processes.
- **kill -9 <process_id>** - This command will allow you to kill a process.
- **rpm -q httpd** - This command will allow you to check if a package is installed.
- **/etc/ssh/sshd_config** - This file contains the configuration for the SSH server.


