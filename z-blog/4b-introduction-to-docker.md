# **Part 5: Introduction to Docker**

In **Part 5** of the **Mastering Microservices** series, we will explore **Docker**, a powerful tool for developing, packaging, and running applications in isolated environments called containers. Docker plays a crucial role in modern microservices architecture by allowing each service to run in its own container, independent of the underlying system.

In this article, you will learn the basics of Docker, how it fits into the microservices ecosystem, and how to use it to package your microservices. By the end, you’ll have a strong understanding of how Docker simplifies development, testing, and deployment in both local and production environments.

---

## **What is Docker?**

**Docker** is an open-source platform that enables developers to automate the deployment of applications inside lightweight, portable containers. A **container** includes everything an application needs to run: code, libraries, dependencies, and configurations. This allows you to run applications consistently across different environments without worrying about system incompatibilities.

In essence, Docker helps you "package" your microservices so they can run anywhere, whether on your local machine, a staging environment, or production servers.

### **Why Docker is Essential for Microservices**

In a microservices architecture, each service is deployed independently. Docker provides several benefits that make it an ideal choice for managing microservices:

1. **Isolation**: Each microservice runs in its own container, isolated from others, ensuring that dependencies don’t conflict.
2. **Portability**: Docker containers can run on any system that supports Docker (Linux, Windows, macOS), making it easy to move applications between environments.
3. **Efficiency**: Docker containers are lightweight compared to virtual machines, allowing you to run multiple containers on the same machine with minimal overhead.
4. **Scalability**: Docker integrates with container orchestration tools like Kubernetes, making it easy to scale microservices as demand increases.

---

## **How Docker Fits into Microservices**

In a typical microservices architecture, each service is containerized using Docker. These containers can then communicate with each other through exposed ports or via a message broker (e.g., Kafka). Docker ensures that each service has the exact environment it needs to run, regardless of the host system.

For example, in our **Conference Microservices Application**, we will use Docker to package and run the following services:

- **Frontend Service**: A Next.js-based web application.
- **C4P Service**: A Go-based backend for handling Call for Papers submissions.
- **Agenda Service**: A Go-based service that manages the conference schedule.
- **Notifications Service**: A Go-based service for sending notifications.

Each of these services will run in its own Docker container, providing a consistent environment for development, testing, and deployment.

---

## **Step 1: Install Docker**

To get started with Docker, you'll need to install it on your system.

### **Install Docker on Windows and macOS**

1. **Docker Desktop**: Docker provides a desktop application for both Windows and macOS. You can download it from [Docker's official website](https://www.docker.com/products/docker-desktop).
2. **Installation**: Follow the instructions provided on the Docker website for installation. Docker Desktop includes Docker Engine, Docker CLI, and Kubernetes for easy container management.

### **Install Docker on Linux**

For Ubuntu/Debian-based systems, follow these steps:

1. **Update the package database**:
   ```bash
   sudo apt update
   ```

2. **Install Docker**:
   ```bash
   sudo apt install docker.io
   ```

3. **Start Docker and enable it to run at startup**:
   ```bash
   sudo systemctl start docker
   sudo systemctl enable docker
   ```

4. **Verify the installation**:
   ```bash
   docker --version
   ```

---

## **Step 2: Basic Docker Commands**

Once Docker is installed, you can start interacting with it using the Docker CLI. Let’s go over some basic Docker commands to help you get familiar with the tool.

### **1. Pull a Docker Image**

Docker images are the foundation of containers. You can think of an image as a template that includes your application, its dependencies, and the environment it runs in. To pull an existing image from **Docker Hub** (a public registry of pre-built images), you can use the `docker pull` command.

For example, let’s pull an official **Go** image:

```bash
docker pull golang:1.18-alpine
```

This command pulls the `golang` image, version `1.18`, based on the Alpine Linux distribution.

### **2. Run a Docker Container**

To run a container from an image, use the `docker run` command. This starts a container and allows you to interact with the application running inside it.

For example, to run a simple Go container:

```bash
docker run -it --rm golang:1.18-alpine sh
```

- **-it**: Runs the container in interactive mode.
- **--rm**: Automatically removes the container when it stops.
- **golang:1.18-alpine**: The image to run.
- **sh**: Starts a shell inside the container.

This command gives you a shell inside a running container based on the Go image. You can exit the container by typing `exit`.

### **3. List Running Containers**

To see all containers that are currently running, use the `docker ps` command:

```bash
docker ps
```

This will show you details about each running container, including its ID, the image it’s based on, and the ports it’s using.

### **4. Stop a Container**

To stop a running container, use the `docker stop` command followed by the container’s ID or name:

```bash
docker stop <container-id>
```

Replace `<container-id>` with the actual ID of the container you want to stop.

### **5. Remove a Container**

To remove a stopped container, use the `docker rm` command:

```bash
docker rm <container-id>
```

This will permanently delete the container from your system.

---

## **Step 3: Writing a Dockerfile**

A **Dockerfile** is a script that defines how a Docker image is built. It contains instructions for setting up the environment, installing dependencies, and copying the application code into the container.

Here’s a simple example of a Dockerfile for a Go-based microservice:

```dockerfile
# Start with a lightweight Go image
FROM golang:1.18-alpine

# Set the working directory inside the container
WORKDIR /app

# Copy the Go module files and download dependencies
COPY go.mod go.sum ./
RUN go mod download

# Copy the rest of the application code
COPY . .

# Build the Go application
RUN go build -o myapp

# Expose the port the application will run on
EXPOSE 8080

# Start the application
CMD ["./myapp"]
```

### **Breaking Down the Dockerfile**:

1. **FROM**: Specifies the base image (in this case, a lightweight Go image based on Alpine Linux).
2. **WORKDIR**: Sets the working directory inside the container.
3. **COPY**: Copies files from your local machine to the container.
4. **RUN**: Executes commands inside the container (e.g., downloading dependencies, building the Go application).
5. **EXPOSE**: Declares the port that the container will use (8080 in this case).
6. **CMD**: Defines the default command to run when the container starts.

### **Building a Docker Image**

To build a Docker image from the Dockerfile, navigate to the directory containing the `Dockerfile` and run:

```bash
docker build -t my-go-app .
```

This command creates an image called `my-go-app`.

### **Running the Docker Image**

After the image is built, you can run it as a container:

```bash
docker run -p 8080:8080 my-go-app
```

- **-p 8080:8080**: Maps port 8080 on your host machine to port 8080 in the container.

Your Go application will now be running in a container, accessible via `http://localhost:8080`.

---

## **Step 4: Managing Multiple Containers**

In microservices, you often have multiple services running in different containers. Docker makes it easy to manage multiple containers by linking them together using **Docker Compose**.

### **What is Docker Compose?**

**Docker Compose** is a tool for defining and running multi-container Docker applications. You can define all the services and their dependencies in a single file, making it easy to start and manage multiple containers at once.

We’ll cover Docker Compose in more detail in a later part of this series.

---

## **Conclusion**

Docker is a powerful tool that simplifies the process of developing, packaging, and running microservices. By containerizing each microservice, Docker ensures consistency across different environments, making your application portable, scalable, and easier to manage. In this article, we’ve covered the basics of Docker, including installing Docker, using basic commands, writing a Dockerfile, and running a containerized application.

In the next part of this series, we’ll dive deeper into packaging microservices into Docker images using a **real-world example**, and introduce Docker Compose for managing multiple microservices in a local environment.

Ready to move forward? Check out [**Part 6: Docker: Package Microservices into Application Image Using Docker**](#) to learn how to containerize your microservices.

---

**GitHub Repository**: [Mastering Microservices with Azure, Docker, Kubernetes, Terraform, and GitHub Actions](https://github.com/cloudikeme/mastering-microservices-with-azure-docker-kubernetes-terraform-github-actions)




