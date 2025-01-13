# cont



Check installations:

# Docker
docker --version
docker run hello-world

# Kubectl
kubectl version --client
kubectl get nodes

# Minikube
minikube version
minikube start --driver=docker
minikube status

# Git
git --version
git clone https://github.com/octocat/Hello-World.git

# Java
java -version
javac -version




Go to 
https://github.com/manikantabandaru/CollegeApp

sudo apt update

sudo apt install git

git --version

git clone https://github.com/manikantabandaru/CollegeApp

Go to the directory.

Exercise 1: Write Dockerfile and run docker image to execute java program

a. In interactive console mode
b. in Deamon mode

Build the Docker image:

docker build -t workshop .

docker images

Run in interactive mode:

docker run -p 8081:8081 workshop

Check on:

http://localhost:8081/workshop

Stop the Docker image by clicking on CTRL + C

Run in daemon mode:

Create the Docker image once again.

docker build -t workshop .

docker run -p 8081:8081 -d workshop

docker ps

Stop the container:

docker stop <CONTAINER_ID>




2. Log into docker container to see logs for debug purpose and locate jars path, locate logs path


Create the Docker file once again.

View logs:

docker logs <CONTAINER_ID>

docker logs -f <CONTAINER_ID>

Log into the container:

docker exec -it <CONTAINER_ID> /bin/sh

Locate files:

find / -name "*.jar"

find / -name "*.log"

Stop the container:

docker stop <CONTAINER_ID>

-----------------------------------------------------------------
Ex. 4

Build the Docker image:

docker build -t workshop .

Run the container:


docker run -p 8082:8082 \
    --env SERVER_PORT=8082 \
    --env UPLOAD_DIR=/tmp/fileupload \
    -v ~/fileupload:/tmp \
    -d workshop
    
Test file upload:

curl --location 'http://localhost:8082/upload' \
    --form 'file=@/home/ayushanand/Docs/CollegeApp/Dockerfile'
    
Check uploaded files:

ls ~/fileupload

Stop the container:

docker stop <CONTAINER_ID>






_________________________________________________________________________________________

Questions:

Basic Questions
1. What is Docker?
Answer: Docker is an open-source platform that allows developers to automate the deployment of applications inside lightweight, portable containers. Containers include the application and its dependencies, ensuring it runs consistently across environments.
2. What are the main components of Docker?
Answer:
Docker Engine: Core service for building and running containers.
Docker Images: Pre-configured environments for applications.
Docker Containers: Instances of Docker images running as isolated processes.
Docker Hub: A cloud-based registry for sharing Docker images.
3. What are the steps to use Docker?
Answer:
Install Docker: Install Docker on your system.
Write a Dockerfile: Define the application and its dependencies.
Build the Docker Image: Use docker build to create an image.
Run a Container: Use docker run to create and start a container.
Test the Application: Access the application via the mapped ports.
Stop the Container: Use docker stop to stop running containers.
4. What is a Dockerfile?
Answer: A Dockerfile is a script that contains a series of instructions to build a Docker image. It specifies the base image, application code, dependencies, and commands to configure the container.
5. What is the difference between Interactive Mode and Daemon Mode?
Answer:
Interactive Mode:

The container runs in the foreground, and logs or output are displayed in the terminal.
Example: docker run -p 8081:8081 workshop
Use Ctrl+C to stop the container.
Daemon Mode:

The container runs in the background, detached from the terminal.
Example: docker run -p 8081:8081 -d workshop
Use docker stop <CONTAINER_ID> to stop it.
6. What are Docker logs?
Answer: Docker logs capture the output (stdout and stderr) of a running container. They help in debugging and monitoring the application inside the container.

To view logs:
bash
Copy code
docker logs <CONTAINER_ID>
To follow logs in real-time:
bash
Copy code
docker logs -f <CONTAINER_ID>
7. How can you access a running container?
Answer: Use the docker exec command to access the shell of a running container:
bash
Copy code
docker exec -it <CONTAINER_ID> /bin/sh
Intermediate Questions
8. What is volume mounting in Docker?
Answer: Volume mounting allows you to map a directory on the host system to a directory inside the container. It enables persistent storage and data sharing between the host and the container.

Example:
bash
Copy code
docker run -v /host/path:/container/path -d workshop
9. What are environment variables in Docker?
Answer: Environment variables are used to configure containers at runtime. They are passed using the --env or -e flag.

Example:
bash
Copy code
docker run --env SERVER_PORT=8082 -d workshop
10. What is the purpose of docker ps?
Answer: The docker ps command lists all currently running containers. To see stopped containers as well, use:
bash
Copy code
docker ps -a
11. What is the difference between Docker Images and Containers?
Answer:
Docker Image:

A static, read-only template used to create containers.
Example: workshop built using docker build.
Docker Container:

A runtime instance of a Docker image, with its own isolated environment.
Example: Running docker run creates a container.
12. How can you stop a running container?
Answer: Use the docker stop command:
bash
Copy code
docker stop <CONTAINER_ID>
13. What is the purpose of docker build?
Answer: The docker build command creates a Docker image from a Dockerfile.

Example:
bash
Copy code
docker build -t workshop .
Advanced Questions
14. What is Minikube, and why is it used?
Answer: Minikube is a tool that runs a single-node Kubernetes cluster on your local machine. It is used for learning, testing, and experimenting with Kubernetes.
15. How can you expose a container’s application to the host?
Answer: Use the -p flag to map container ports to host ports:
bash
Copy code
docker run -p 8081:8081 workshop
16. What is Kubernetes, and how does it relate to Docker?
Answer: Kubernetes is an open-source platform for automating deployment, scaling, and management of containerized applications. Docker is used to create and manage containers, while Kubernetes orchestrates them.
17. What is the purpose of docker logs vs kubectl logs?
Answer:
docker logs: Retrieves logs from a Docker container.
kubectl logs: Retrieves logs from a pod running in a Kubernetes cluster.
Practical Questions
18. How do you verify if a Docker container is running?
Answer: Use the docker ps command. It lists all running containers.
19. How can you test a file upload endpoint in a container?
Answer: Use the curl command:
bash
Copy code
curl --location 'http://localhost:8082/upload' --form 'file=@/path/to/file.txt'



