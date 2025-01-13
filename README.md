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

