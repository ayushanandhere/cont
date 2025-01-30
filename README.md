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
______________________________________________________________________________

Exercise 1: Write Dockerfile and run docker image to execute java program

a. In interactive console mode
b. in Deamon mode


docker build -t workshop .

docker images

->  interactive mode:

docker run -p 8081:8081 workshop

Check on:

http://localhost:8081/workshop

Stop the Docker image by clicking on CTRL + C

-> Run in daemon mode:

docker run -p 8081:8081 -d workshop

docker ps

-> Stop the container:

docker stop <CONTAINER_ID>


______________________________________________________________________________________________________

2. Log into docker container to see logs for debug purpose and locate jars path, locate logs path


docker build -t workshop .

docker run -p 8081:8081 -d workshop 

docker logs <CONTAINER_ID>

docker logs -f <CONTAINER_ID>

-> Log into the container:

docker exec -it <CONTAINER_ID> /bin/sh

-> Locate files:

find / -name "*.jar"

find / -name "*.log"

-> Stop the container:

docker stop <CONTAINER_ID>

____________________________________________________________________

Ex 3. Run the Java program with environment variables

docker build -t workshop .

docker run -p 8082:8082 --env SERVER_PORT=8082 -d workshop

http://localhost:8082/workshop

docker stop <CONTAINER_ID>

-----------------------------------------------------------------
Ex. 4

docker build -t workshop .

mkdir -p /home/ayushanand/Docs/newdir


Run the container:

docker run -p 8082:8082 \
  --env SERVER_PORT=8082 \
  --env UPLOAD_DIR=/tmp/newdir \
  -v /home/ayushanand/Docs/newdir:/tmp/newdir \
  -d workshop

http://localhost:8082/workshop

    
-> Test file creation:

echo "Hello from host" > /home/ayushanand/Docs/newdir/testfile.txt

-> Upload

curl --location 'http://localhost:8082/upload' \
  --form 'file=@"/home/ayushanand/Docs/newdir/testfile.txt"'

    
Check uploaded files:

ls /home/ayushanand/Docs/newdir

Stop the container:

docker stop <CONTAINER_ID>


_________________________________________________________________________________________



## 1. What is Docker?
**Answer**:  
Docker is an open-source platform that automates the deployment of applications inside lightweight containers. These containers package the application and its dependencies, ensuring consistent behaviour across different environments.

---

## 2. What are the main components of Docker?
**Answer**:  
- **Docker Engine**: The core service for building and running containers.  
- **Docker Images**: Pre-configured environments (templates) for applications.  
- **Docker Containers**: Running instances of Docker images, providing isolated environments.  
- **Docker Hub**: A cloud-based registry for finding and sharing Docker images.

---

## 3. What are the steps to use Docker?
**Answer**:
1. **Install Docker** on your system.  
2. **Write a Dockerfile** describing the application and its dependencies.  
3. **Build the Docker Image** using `docker build`.  
4. **Run a Container** using `docker run`.  
5. **Test the Application** via mapped ports in the browser or a tool like curl.  
6. **Stop the Container** using `docker stop`.

---

## 4. What is a Dockerfile?
**Answer**:  
A Dockerfile is a text file containing instructions to build a Docker image. It specifies the base image, the application code, dependencies, and any necessary commands to configure and run the application inside a container.

---

## 5. What is the difference between Interactive Mode and Daemon Mode?
**Answer**:

- **Interactive Mode**  
  - The container runs in the foreground.  
  - Logs appear directly in the terminal.  
  - Example: `docker run -p 8081:8081 workshop`  
  - Stop with **Ctrl + C**.

- **Daemon Mode**  
  - The container runs in the background (detached).  
  - Example: `docker run -p 8081:8081 -d workshop`  
  - Stop with `docker stop <CONTAINER_ID>`.

---



