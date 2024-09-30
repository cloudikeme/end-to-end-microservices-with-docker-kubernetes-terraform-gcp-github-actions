# **Part 4: Difference Between Containers and Images**

In **Part 4** of the **Mastering Microservices** series, we’ll explore the key concepts of **containers** and **images**, which are essential for building and running microservices-based applications. Understanding the difference between these two is crucial for anyone working with tools like Docker or Kubernetes, as they form the backbone of how microservices are deployed, managed, and scaled in both local and production environments.

---

## **What Are Containers and Images?**

At a high level, **containers** and **images** are closely related but serve different purposes in application development and deployment. Let’s break them down:

- **Images**: A container image is a **blueprint** or **template** that contains everything your application needs to run, including the application code, runtime environment, libraries, and dependencies.
  
- **Containers**: A container is a **running instance** of an image. When you run an image, it creates a container that provides the isolated environment for your application to execute.

---

## **Understanding Container Images**

### **What is a Container Image?**

A **container image** is a static, read-only package that includes all the necessary files, libraries, and configurations needed to run an application. It contains everything from the operating system (e.g., Linux) to the application code, and even dependencies. Think of it as a **blueprint** for creating a container.

### **Components of a Container Image**

1. **Base Operating System**: A minimal OS like Ubuntu, Alpine, or Debian that your application runs on.
2. **Application Code**: The actual code for your microservice, such as a Go or Node.js application.
3. **Dependencies**: Libraries, packages, and tools required by the application (e.g., a web framework, database drivers).
4. **Configuration Files**: Environmental configurations and setup scripts needed for running the application.
5. **Dockerfile**: The file used to define and build a container image.

### **Example of a Dockerfile**

Here’s a simple example of a **Dockerfile** that creates an image for a Go-based microservice:

```dockerfile
# Use an official Go image as the base image
FROM golang:1.18-alpine

# Set the working directory inside the container
WORKDIR /app

# Copy the Go module files and the rest of the app source code
COPY go.mod go.sum ./
RUN go mod download
COPY . .

# Build the Go application
RUN go build -o my-microservice

# Expose the port the app runs on
EXPOSE 8080

# Run the Go app
CMD ["./my-microservice"]
```

- **FROM**: This specifies the base image (Go in this case) to build upon.
- **WORKDIR**: Sets the working directory inside the container.
- **COPY**: Copies files from the host machine to the container image.
- **RUN**: Executes commands (e.g., downloading dependencies, building the app).
- **EXPOSE**: Declares the port that the container will listen on.
- **CMD**: Defines the command to run when the container starts.

### **Building and Running a Docker Image**

1. **Build an Image**:
   After writing a `Dockerfile`, you can build an image with:

   ```bash
   docker build -t my-microservice .
   ```

   This command will create a new image called `my-microservice`.

2. **List Docker Images**:
   You can list all your images with:

   ```bash
   docker images
   ```

   This will display all the container images available on your machine, including the image ID, tag, and size.

---

## **Understanding Containers**

### **What is a Container?**

A **container** is a **running instance** of a container image. It represents an isolated environment where your application runs. Containers abstract away the complexities of system dependencies and environment configurations, making it easy to deploy applications across different platforms without worrying about compatibility issues.

### **How Containers Work**

Containers leverage technologies like **Linux namespaces** and **cgroups** to isolate the application’s processes from the rest of the system, providing a lightweight virtualized environment. Unlike traditional virtual machines, containers share the host machine’s kernel but keep the application and its dependencies isolated, which leads to faster performance and lower resource usage.

### **Creating and Running a Container**

Once you have an image, you can create and run a container using the `docker run` command.

1. **Run a Container**:

   ```bash
   docker run -d -p 8080:8080 my-microservice
   ```

   This command:
   - **-d**: Runs the container in detached mode (in the background).
   - **-p 8080:8080**: Maps port 8080 of the host machine to port 8080 in the container.
   - `my-microservice`: The name of the image you’re using to create the container.

2. **List Running Containers**:
   To list running containers, use:

   ```bash
   docker ps
   ```

   This command will show all containers currently running, along with their ID, status, and the ports they are using.

3. **Stop a Running Container**:
   To stop a running container:

   ```bash
   docker stop <container-id>
   ```

   Replace `<container-id>` with the ID or name of the container.

---

## **Key Differences Between Containers and Images**

While containers and images are closely related, they serve different purposes. Here’s a breakdown of the key differences:

| **Aspect**              | **Container Image**                                         | **Container**                                           |
|-------------------------|-------------------------------------------------------------|---------------------------------------------------------|
| **Definition**           | A static, read-only file containing the application, libraries, and environment. | A running instance of a container image.                |
| **State**                | Read-only; cannot be modified after creation.               | Mutable; data and processes can change during runtime.   |
| **Lifecycle**            | Exists until deleted or replaced with a new version.        | Runs as long as the process inside is active; can be stopped or restarted. |
| **Purpose**              | Acts as a blueprint or template for creating containers.     | Provides an isolated environment for running applications. |
| **Creation**             | Created from a `Dockerfile` or another image.               | Created by running an image with `docker run`.           |
| **Storage**              | Stored on disk and can be shared across environments.       | Exists in memory or on disk while running.               |

---

## **Real-World Example: Using Containers in Microservices**

In a microservices architecture, each service is typically packaged into its own container image. These images are then deployed as containers in various environments (e.g., local development, staging, production).

For instance, in our **Conference Microservices Application**, we have several microservices:

- **Frontend Service** (Next.js)
- **C4P Service** (Go)
- **Agenda Service** (Go)
- **Notifications Service** (Go)

Each of these services will have its own Docker image, created from a `Dockerfile`. When deployed, these images will run as containers, each providing an isolated environment to execute the service.

For example:
1. **Frontend Service** will run in one container, exposing port `3000` for the web interface.
2. **C4P Service** will run in another container, handling requests to `http://localhost:3001/submit`.
3. **Agenda Service** will manage the conference schedule in a separate container on `http://localhost:3002/agenda`.
4. **Notifications Service** will handle sending notifications from a separate container.

---

## **Conclusion**

To sum up, the **image** is a static, packaged blueprint of your application and its dependencies, while the **container** is the running instance of that image, providing an isolated environment for your application. Understanding the distinction between these two concepts is key to mastering microservices deployment and containerized development.

In the next part of this series, we will explore how to package your microservices into Docker images and run them as containers using Docker. We’ll cover how to write effective Dockerfiles, optimize images, and manage multiple containers.

Ready to move forward? Check out [**Part 5: Introduction to Docker**](#) to start working with Docker and containerize your microservices.

---

**GitHub Repository**: [Mastering Microservices with Azure, Docker, Kubernetes, Terraform, and GitHub Actions](https://github.com/cloudikeme/mastering-microservices-with-azure-docker-kubernetes-terraform-github-actions)