


# **Part 6: Docker: Package Microservices into Application Image Using Docker**

Welcome to **Part 6** of the **Mastering Microservices** series. In this article, you’ll learn how to **package microservices into Docker images**. Containerizing microservices with Docker ensures each service has its own isolated environment with all the dependencies it needs to run. This makes it easy to develop, test, and deploy microservices across different environments.

By the end of this article, you’ll understand how to create **Docker images** for the **Conference Microservices Application**, using Dockerfiles for each service.

---

## **Why Package Microservices into Docker Images?**

Containerizing microservices into Docker images offers several advantages:

1. **Consistency**: Every microservice has its own environment, eliminating issues caused by differences in development, staging, or production environments.
2. **Portability**: Docker images can run on any machine that supports Docker, regardless of the underlying OS.
3. **Isolation**: Each microservice runs independently, with its own dependencies and configurations.
4. **Scalability**: Containers are lightweight, making it easy to scale microservices up or down as needed.

In this article, we will package the **Frontend**, **C4P (Call for Papers) Service**, **Agenda Service**, and **Notifications Service** into Docker images.

---

## **Step 1: Write Dockerfiles for Each Microservice**

A **Dockerfile** is a text file that contains instructions for building a Docker image. Each microservice will have its own Dockerfile, specifying the environment, dependencies, and instructions to run the service.

### **1. Frontend Service (Next.js)**

The **Frontend Service** is built using **Next.js**. Here's the Dockerfile for the frontend:

1. Navigate to the `services/frontend/frontend-app/` directory.
2. Create a `Dockerfile`:

   ```bash
   touch Dockerfile
   ```

3. Add the following content to the Dockerfile:

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

### **2. C4P (Call for Papers) Service (Go)**

For the **C4P Service**, which is written in **Go**, you’ll need a Dockerfile that compiles the Go code and sets up a container to run it.

1. Navigate to the `services/c4p-service/` directory.
2. Create a `Dockerfile`:

   ```bash
   touch Dockerfile
   ```

3. Add the following content to the Dockerfile:

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

### **3. Agenda Service (Go)**

The **Agenda Service**, also written in **Go**, will have a similar Dockerfile to the C4P Service:

1. Navigate to the `services/agenda-service/` directory.
2. Create a `Dockerfile`:

   ```bash
   touch Dockerfile
   ```

3. Add the following content:

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

### **4. Notifications Service (Go)**

The **Notifications Service**, which uses Kafka for messaging, will also be written in Go:

1. Navigate to the `services/notifications-service/` directory.
2. Create a `Dockerfile`:

   ```bash
   touch Dockerfile
   ```

3. Add the following content:

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

## **Step 2: Build Docker Images for Each Microservice**

Now that the Dockerfiles are ready, you can build Docker images for each microservice. To do this, navigate to the respective service directory and run the `docker build` command.

### **1. Build the Frontend Image**

1. Navigate to the `frontend-app/` directory:

   ```bash
   cd services/frontend/frontend-app
   ```

2. Build the Docker image:

   ```bash
   docker build -t conference-frontend .
   ```

This will create an image named `conference-frontend`.

### **2. Build the C4P Service Image**

1. Navigate to the `c4p-service/` directory:

   ```bash
   cd ../../c4p-service
   ```

2. Build the Docker image:

   ```bash
   docker build -t c4p-service .
   ```

### **3. Build the Agenda Service Image**

1. Navigate to the `agenda-service/` directory:

   ```bash
   cd ../agenda-service
   ```

2. Build the Docker image:

   ```bash
   docker build -t agenda-service .
   ```

### **4. Build the Notifications Service Image**

1. Navigate to the `notifications-service/` directory:

   ```bash
   cd ../notifications-service
   ```

2. Build the Docker image:

   ```bash
   docker build -t notifications-service .
   ```

---

## **Step 3: Running the Microservices as Containers**

After building the Docker images, you can run each microservice as a container. Use the `docker run` command to start the containers and map the necessary ports.

### **1. Run the Frontend Container**

```bash
docker run -d -p 3000:3000 conference-frontend
```

This command runs the **Frontend** service in detached mode (`-d`) and maps port `3000` of the host to port `3000` of the container.

### **2. Run the C4P Service Container**

```bash
docker run -d -p 3001:3001 c4p-service
```

This runs the **C4P Service** and maps port `3001`.

### **3. Run the Agenda Service Container**

```bash
docker run -d -p 3002:3002 agenda-service
```

This runs the **Agenda Service** on port `3002`.

### **4. Run the Notifications Service Container**

```bash
docker run -d -p 3003:3003 notifications-service
```

This runs the **Notifications Service** on port `3003`.

---

## **Step 4: Verify the Running Containers**

To check if all the containers are running correctly, use the `docker ps` command:

```bash
docker ps
```

This command will list all running containers along with their respective IDs, ports, and status.

---

## **Step 5: Test the Microservices**

Now that the microservices are running as containers, you can interact with them via their respective endpoints.

- **Frontend Service**: Open your browser and go to `http://localhost:3000` to view the frontend of the conference application.
- **C4P Service**: Send a POST request to `http://localhost:3001/submit` to submit a talk proposal.
- **Agenda Service**: Access the agenda at `http://localhost:3002/agenda`.
- **Notifications Service**: Test sending notifications by sending a POST request to `http://localhost:3003/notify`.

---

Checking the container
checking the microservice
debugging the container
stopping the container
removing the container

## **Conclusion**

In this article, we’ve learned how to containerize microservices by writing **Dockerfiles** for each service and building Docker images. We then ran these images as containers, ensuring each microservice is isolated and has all the necessary dependencies. By containerizing your microservices, you make your application easier to manage, scale, and deploy in various environments.

In the next part of the series, we’ll introduce **Docker Compose**, a tool that makes it easy to run multiple containers at once, simplifying local development
