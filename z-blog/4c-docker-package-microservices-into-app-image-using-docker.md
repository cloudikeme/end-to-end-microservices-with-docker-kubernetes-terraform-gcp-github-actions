# Part 6: Docker: Packaging Microservices into Application Images

Welcome to **Part 6** of the **Mastering Microservices** series. In this article, we will explore the process of packaging microservices into Docker images. Containerizing microservices with Docker ensures that each service operates within its own isolated environment, complete with all the necessary dependencies. This approach significantly simplifies the development, testing, and deployment of microservices across diverse environments.

By the end of this article, we will have gained a comprehensive understanding of creating Docker images for the Conference Microservices Application.

---

## Why Package Microservices into Docker Images?

Containerizing microservices into Docker images offers several key advantages:

1.  **Consistency:** Docker provides each microservice with its own self-contained environment, eliminating inconsistencies that may arise from differences between development, staging, or production environments.

2.  **Portability:** Docker images are designed to run seamlessly on any machine equipped with Docker support, regardless of the underlying operating system.

3.  **Isolation:** Each microservice functions independently within its container, isolating its dependencies and configurations from other parts of the application.

4.  **Scalability:** The lightweight nature of containers enables effortless scaling of microservices up or down to meet fluctuating demands.

In this article, we will focus on packaging the **Frontend**, **C4P (Call for Papers) Service**, **Agenda Service**, and **Notifications Service** into Docker images.

---

## Step 1: Crafting Dockerfiles for Each Microservice

A **Dockerfile** serves as a blueprint, providing instructions for building a Docker image. Each microservice will have its dedicated Dockerfile, meticulously outlining the environment, dependencies, and commands needed to run the service.

### 1. Frontend Service (Next.js)

The **Frontend Service**, built using Next.js, requires a Dockerfile to package it into a Docker image.

We'll create a file named *Dockerfile* with the following content within the *services/frontend/frontend-app/* directory:

```dockerfile
# Use the official Node.js image as the base
FROM node:16-alpine

# Set the working directory inside the container
WORKDIR /app

# Copy the package.json and package-lock.json
COPY package*.json ./

# Install the dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the Next.js application
RUN npm run build

# Expose the port the app will run on
EXPOSE 3000

# Start the Next.js application
CMD ["npm", "run", "start"]
```

### 2. C4P (Call for Papers) Service (Go)

The **C4P Service**, implemented in Go, necessitates a Dockerfile that compiles the Go code and sets up the container environment for execution.

We'll navigate to the *services/c4p-service/* directory and create a *Dockerfile* with the following instructions:

```dockerfile
# Use the official Go image as the base image
FROM golang:1.18-alpine

# Set the working directory inside the container
WORKDIR /app

# Copy the Go module files and download dependencies
COPY go.mod go.sum ./
RUN go mod download

# Copy the rest of the application code
COPY . .

# Build the Go application
RUN go build -o c4p-service

# Expose the port the service will run on
EXPOSE 3001

# Run the Go application
CMD ["./c4p-service"]
```

### 3. Agenda Service (Go)

Similar to the C4P Service, the **Agenda Service**, also written in Go, will have a comparable Dockerfile.

Navigating to the *services/agenda-service/* directory, we'll create a *Dockerfile* containing the following:

```dockerfile
# Use the official Go image
FROM golang:1.18-alpine

# Set the working directory inside the container
WORKDIR /app

# Copy the Go module files and download dependencies
COPY go.mod go.sum ./
RUN go mod download

# Copy the rest of the application code
COPY . .

# Build the Go application
RUN go build -o agenda-service

# Expose the port the service will run on
EXPOSE 3002

# Run the Go application
CMD ["./agenda-service"]
```

### 4. Notifications Service (Go)

The **Notifications Service**, relying on Kafka for messaging, is also implemented in Go and will have its own Dockerfile.

Within the *services/notifications-service/* directory, we'll create a *Dockerfile* with these commands:

```dockerfile
# Use the official Go image
FROM golang:1.18-alpine

# Set the working directory inside the container
WORKDIR /app

# Copy the Go module files and download dependencies
COPY go.mod go.sum ./
RUN go mod download

# Copy the rest of the application code
COPY . .

# Build the Go application
RUN go build -o notifications-service

# Expose the port the service will run on
EXPOSE 3003

# Run the Go application
CMD ["./notifications-service"]
```

---

## Step 2: Building Docker Images

With our Dockerfiles in place, we can now proceed to build the Docker images for each microservice. This involves navigating to the respective service directory and executing the appropriate *docker build* command.

### 1. Building the Frontend Image

Let's start by building the Frontend image.

From the *frontend-app/* directory:

```bash
$ docker build -t conference-frontend .
```

This command will create a Docker image named `conference-frontend`.

### 2. Building the C4P Service Image

Next, we'll build the C4P Service image.

```bash
$ docker build -t c4p-service .
```

### 3. Building the Agenda Service Image

Moving on to the Agenda Service image:

```bash
$ docker build -t agenda-service .
```

### 4. Building the Notifications Service Image

Finally, we'll build the Notifications Service image:

```bash
$ docker build -t notifications-service .
```

---

## Step 3: Running Microservices as Containers

Now that we have our Docker images, we can run each microservice as a container. The *docker run* command allows us to start the containers and map the required ports.

### 1. Running the Frontend Container

We can run the **Frontend** service using the following command:

```bash
$ docker run -d -p 3000:3000 conference-frontend
```

This command launches the **Frontend** service in detached mode (`-d`) and maps port `3000` on the host machine to port `3000` within the container.

### 2. Running the C4P Service Container

Let's run the **C4P Service** container:

```bash
$ docker run -d -p 3001:3001 c4p-service
```

This command starts the **C4P Service** and maps port `3001`.

### 3. Running the Agenda Service Container

Now, we'll run the **Agenda Service** container:

```bash
$ docker run -d -p 3002:3002 agenda-service
```

This command launches the **Agenda Service** and maps port `3002`.

### 4. Running the Notifications Service Container

Lastly, we'll run the **Notifications Service** container:

```bash
$ docker run -d -p 3003:3003 notifications-service
```

This command starts the **Notifications Service** and maps port `3003`.

---

## Step 4: Verifying Running Containers

To verify that all containers are running as expected, we can use the *docker ps* command:

```bash
$ docker ps
```

This command provides a list of all currently running containers, displaying their IDs, mapped ports, and status.

---

## Step 5: Checking Container Logs

To troubleshoot or inspect the behavior of a specific container, we can examine its logs using the *docker logs* command, followed by the container ID or name:

```bash
$ docker logs <container-id-or-name>
```

For example, to view the logs of the frontend container, you might use:

```bash
$ docker logs conference-frontend 
```

## Step 6: Accessing a Container's Shell

Sometimes, you might need to interact directly with a running container's shell for debugging or running commands. We can achieve this using the *docker exec* command: 

```bash
$ docker exec -it <container-id-or-name> /bin/sh
```

Replace `<container-id-or-name>` with the actual container ID or name. The *-it* flags enable an interactive terminal session.

## Step 7: Stopping Running Containers

When we need to halt a running container, we can use the *docker stop* command, specifying the container ID or name:

```bash
$ docker stop <container-id-or-name>
```

### Step 8: Removing Containers

To remove a container, we can use the *docker rm* command: 

```bash
$ docker rm <container-id-or-name>
``` 

---

## Step 9: Testing the Microservices

With our microservices up and running as containers, we can now interact with them through their respective endpoints.

- **Frontend Service:** Access the frontend of the conference application in your web browser at `http://localhost:3000`.
- **C4P Service:**  Submit a talk proposal by sending a POST request to `http://localhost:3001/submit`.
- **Agenda Service:**  View the conference agenda at `http://localhost:3002/agenda`.
- **Notifications Service:**  Send test notifications by issuing a POST request to `http://localhost:3003/notify`.

---

## Conclusion

In this article, we've walked through the process of containerizing microservices. We learned how to create Dockerfiles, build images, run those images as containers, check container logs, access container shells, and manage the lifecycle of our containers. This approach ensures each service operates within its isolated environment, equipped with all the required dependencies. By containerizing our microservices, we gain significant advantages in managing, scaling, and deploying our application across different environments.

In the next part of this series, we will delve into **Docker Compose**, a powerful tool that simplifies the management of multi-container applications.

