## Docker

Before going into Docker, Let's understand How companies used to deploy application in a server. They have different methods to deploy application:
- We can use Bare metal server, In Bare metal server, We are going to install operating system in the server and then we are going to install all the dependencies and then we are going to run our application in the server. If our application crashes, It will make our application down for 30 minutes to 1 hour.
- We can use Virtual machine, We are going to use Virtual machines in cloud, Behind the scenes, Hypervisors are used to create virtual machines and then we are going to install operating system in the Virtual machine and then we are going to install all the dependencies and then we are going to run our application in the virtual machine. If our application crashes, It will make our application down for alteast 5 minutes.
- So to overcome this problem, We are going to use Docker. In Docker, We are going to Create Docker image and then we are going to use the Docker image to run  the Docker container. If our application crashes, It will make our application down for Less than 1 second.

### What is Docker?

Docker is a tool designed to make it easier to create, deploy, and run applications by using containers. Containers allow a developer to package up an application with all of the parts it needs, such as libraries and other dependencies, and ship it all out as one package.

### What is Docker Image?

Docker Image is a template for creating Docker container. We can create Docker image by using Dockerfile or by using docker commit command. It is like a Package which contains all the dependencies and libraries required to run the application.

### What is Docker Container?

Docker Container is a running instance of Docker image. We can create Docker container by using Docker image. It is like a Virtual machine but it is not a Virtual machine.<br>

For more reference, [Click Here](https://www.docker.com/resources/what-container/)<br>

Normally, When We are using Windows it uses ISO file to install the operating system. That ISO file is like a Docker image. When we are installing the operating system, It will create a Virtual machine. That Virtual machine is like a Docker container.

### Docker Commands

- **docker version** : It will show the docker version.
- **docker info** : It will show the docker information.
- **docker images** : It will show all the docker images.
- **docker ps** : It will show all the running docker containers.
- **docker ps -a** : It will show all the docker containers.
- **docker pull <image-name>** : It will pull the docker image from the docker hub.
- **docker run <image-name>** : It will run the docker image and create the docker container.
- **docker run -it <image-name>** : It will run the docker image and create the docker container and it will open the terminal in the docker container.
- **docker run -it -d <image-name>** : It will run the docker image and create the docker container and it will run the docker container in the background.
- **docker run -it -d -p 8080:80 <image-name>** : It will run the docker image and create the docker container and it will run the docker container in the background and it will map the port 8080 of the host machine to the port 80 of the docker container.
- **docker attach <container-id>** : It will attach the terminal to the docker container.
- **docker exec -it <container-id> bash** : It will open the terminal in the docker container.
- **docker stop <container-id>** : It will stop the docker container.
- **docker start <container-id>** : It will start the docker container.
- **docker rm <container-id>** : It will delete the docker container.
- **docker rmi <image-id>** : It will delete the docker image.
- **docker commit <container-id> <image-name>** : It will create the docker image from the docker container.
- **docker rm -f <container-id>** : It will delete the docker container forcefully.
- **docker rm -f $(docker ps -a -q)** : It will delete all the docker containers forcefully.
- **docker rmi -f <image-id>** : It will delete the docker image forcefully.
- **netstat -tnlp** : It will show all the ports which are running in the host machine.
- **ctrl+p+q** : It will detach the terminal from the docker container.

