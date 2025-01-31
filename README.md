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






## 6. What are Docker logs?
**Answer**:  
Docker logs capture the output (`stdout` and `stderr`) of a running container, which is crucial for debugging and monitoring.

- **View logs**:
  ```bash
  docker logs <CONTAINER_ID>
Follow logs:
bash
Copy
Edit
docker logs -f <CONTAINER_ID>
7. How can you access a running container?
Answer:
Use docker exec to open a shell session inside a running container:

bash
Copy
Edit
docker exec -it <CONTAINER_ID> /bin/sh
8. What is volume mounting in Docker?
Answer:
Volume mounting maps a folder on the host to a folder inside the container, enabling persistent storage and data sharing:

bash
Copy
Edit
docker run -v /host/path:/container/path -d workshop
9. What are environment variables in Docker?
Answer:
They allow you to configure a container at runtime. You can pass them using --env (or -e):

bash
Copy
Edit
docker run --env SERVER_PORT=8082 -d workshop
10. What is the purpose of docker ps?
Answer:
docker ps lists all currently running containers.
Use docker ps -a to see both running and stopped containers.

11. What is the difference between Docker Images and Containers?
Answer:

Docker Images: Read-only templates used to create containers.
Docker Containers: Runtime instances of those images, offering an isolated environment where the application runs.
12. How can you stop a running container?
Answer:

bash
Copy
Edit
docker stop <CONTAINER_ID>
13. What is the purpose of docker build?
Answer:
docker build creates a Docker image from a Dockerfile:

bash
Copy
Edit
docker build -t workshop .
14. What is Minikube, and why is it used?
Answer:
Minikube lets you run a single-node Kubernetes cluster on your local machine. It’s mainly used for learning, testing, and development without requiring a full multi-node setup.

15. How can you expose a container’s application to the host?
Answer:
Use the -p option to map the container port to a host port:

bash
Copy
Edit
docker run -p 8081:8081 workshop
16. What is Kubernetes, and how does it relate to Docker?
Answer:
Kubernetes is an open-source system for automating deployment, scaling, and managing containerized applications. Docker creates and runs containers, while Kubernetes orchestrates and manages them across multiple nodes.

17. What is the purpose of docker logs vs kubectl logs?
Answer:

docker logs: Retrieves logs from a local Docker container.
kubectl logs: Retrieves logs from a pod running in a Kubernetes cluster.
18. How do you verify if a Docker container is running?
Answer:
Use:

bash
Copy
Edit
docker ps
It lists all active (running) containers.

19. How can you test a file upload endpoint in a container?
Answer:
Use curl to post a file to the /upload endpoint:

bash
Copy
Edit
curl --location 'http://localhost:8082/upload' \
  --form 'file=@"/path/to/file.txt"'
Copy
Edit






You said:
What is a Docker file and how to build it?
ChatGPT

Thought for a second
A Dockerfile is a text file containing step-by-step instructions for building a Docker image. It specifies:

Base Image (e.g., FROM openjdk:17-jdk-slim)
Application Files to copy or add (e.g., COPY commands)
Environment Setup (e.g., setting environment variables, installing packages)
Startup Command (e.g., ENTRYPOINT or CMD to run your application)
Example Dockerfile
dockerfile
Copy
Edit
# Base image
FROM openjdk:17-jdk-slim

# Working directory
WORKDIR /app

# Copy your jar into the container
COPY demo-1.0.0-SNAPSHOT.jar app.jar

# Expose the port your app will run on
EXPOSE 8080

# Run the application
ENTRYPOINT ["java", "-jar", "app.jar"]
How to Build the Docker Image
Create or open a folder with your Dockerfile (and any app files).

Open a terminal in that folder.

Run:

bash
Copy
Edit
docker build -t my-app .
-t my-app gives the image a name (or “tag”).
. indicates that the Dockerfile is in the current directory.
Once built, you can run the image as a container:

bash
Copy
Edit
docker run -p 8080:8080 my-app






You said:
Tell me about Kubernetes in details and how to work with it.
ChatGPT

Thought for a second
Below is an overview of Kubernetes, its core concepts, and the basic workflow for working with it.

What is Kubernetes?
Kubernetes (often abbreviated as K8s) is an open-source platform designed to automate the deployment, scaling, and management of containerized applications. It provides a distributed system to run containers (often Docker containers) across a cluster of machines, ensuring high availability, scalability, and fault-tolerance.

Key Advantages
Scalability: Easily scale applications up or down.
Portability: Abstracts away the underlying infrastructure (on-premise, cloud, hybrid).
High Availability: Self-healing (restarts failed containers, replaces dead nodes).
Load Balancing & Service Discovery: Built-in ways to route and distribute traffic.
Kubernetes Architecture
Kubernetes follows a master-worker (or control plane - node) architecture.

Control Plane (Master)

API Server: The front end of the control plane; all requests (kubectl, UI, other services) go through it.
etcd: A key-value store for the cluster’s configuration and state.
Controller Manager: Watches the cluster’s desired state vs. actual state, and attempts to reconcile any differences.
Scheduler: Decides which nodes (workers) should run new or unassigned containers (Pods).
Worker Nodes

Kubelet: An agent that communicates with the control plane, ensuring Pods are running.
Container Runtime: Software to run containers (e.g. Docker, containerd).
Kube-Proxy: Manages networking and load balancing for services on each node.
Key Kubernetes Objects
Pod

The smallest deployable unit in Kubernetes.
Usually contains one container (though can contain multiple closely related containers).
Deployment

A higher-level abstraction over Pods.
Defines how many replicas you want, how to roll out changes, and how to roll back if needed.
Service

A stable, permanent IP and DNS name for a set of Pods.
Provides load balancing (e.g., ClusterIP, NodePort, LoadBalancer).
ReplicaSet

Maintains the correct number of Pod replicas.
Usually managed by Deployments behind the scenes.
Namespace

Logical cluster grouping to isolate resources.
Good for environment separation (e.g., dev, test, prod).
ConfigMap & Secret

ConfigMap: Stores configuration data in key-value pairs.
Secret: Stores sensitive data (like passwords) in base64-encoded form.
Ingress (optional add-on)

Manages external access to services within the cluster.
Provides routing, SSL termination, etc.
Basic Kubernetes Workflow
Containerize Your Application

Typically with Docker.
Push the resulting image to a registry (e.g., Docker Hub, AWS ECR, GCP Container Registry).
Install/Set Up Kubernetes

For local development, use Minikube or kind (Kubernetes in Docker).
For production, you might have a managed service (EKS, GKE, AKS) or self-hosted cluster.
Create Configuration YAML Files

Example: A Deployment YAML to define your application Pod specs and replicas.
Example: A Service YAML to define how to expose the Pods internally or externally.
Apply the YAMLs

Using kubectl commands to interact with the cluster:
bash
Copy
Edit
kubectl apply -f my-deployment.yaml
kubectl apply -f my-service.yaml
Verify

Check if your Pods are running:
bash
Copy
Edit
kubectl get pods
Check if your Services are created:
bash
Copy
Edit
kubectl get services
Check overall resources:
bash
Copy
Edit
kubectl get all
Scaling

Adjust the replica count in your Deployment YAML or use kubectl scale:
bash
Copy
Edit
kubectl scale deployment my-app --replicas=5
Updating Your App

Update the container image version in the Deployment YAML or use kubectl set image:
bash
Copy
Edit
kubectl set image deployment/my-app my-container=my-image:v2
Rolling Back

If something goes wrong, you can roll back to a previous version:
bash
Copy
Edit
kubectl rollout undo deployment/my-app
Example of Deployment YAML
Below is a minimal YAML to create a Deployment and a Service:

yaml
Copy
Edit
# my-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-container
        image: my-dockerhub-account/my-image:latest
        ports:
        - containerPort: 8080
        env:
        - name: SERVER_PORT
          value: "8080"
yaml
Copy
Edit
# my-service.yaml
apiVersion: v1
kind: Service
metadata:
  name: my-app-service
spec:
  selector:
    app: my-app
  ports:
  - protocol: TCP
    port: 80        # Service port
    targetPort: 8080  # Container port
  type: NodePort   # Exposes the service on a static port on each node's IP
Apply them:

bash
Copy
Edit

kubectl apply -f my-deployment.yaml
kubectl apply -f my-service.yaml
Tips for Working with Kubernetes

Use Minikube or kind for a local environment if you’re just starting out.
Familiarize yourself with kubectl commands (e.g., kubectl get pods, kubectl describe pod, kubectl logs).
Keep your manifests in version control so you can track changes over time.
Namespace Management: If you use multiple environments (dev, test, prod), separate them by namespaces.
Monitoring & Logging: Tools like Prometheus, Grafana, ELK Stack (Elasticsearch, Logstash, Kibana) can help you keep track of cluster performance and logs.
Use a Managed Service (GKE, EKS, AKS) for production if you don’t want to manage your own control plane.

