# **Part 2: Create a Repository from Linux Terminal Using Git and GitHub CLI**

In **Part 2** of the **Mastering Microservices** series, we’ll set up version control for your microservices project using Git and GitHub. This step is crucial for managing your codebase and collaborating effectively on a complex project like a microservices application. You will create a repository, organize your project structure, and push the initial code to GitHub.

For this tutorial, we’ll use Git and GitHub CLI (`gh`) from the Linux terminal, which works seamlessly in environments like WSL (Windows Subsystem for Linux) or a Linux VM.

---

## **Repository Name for the Project**

Since this is a microservices project, we want the repository name to be descriptive and related to the project. For this tutorial, we will name the repository:

```bash
conference-microservices-app
```

This name makes it clear that the repository contains the code for a microservices-based conference application, which includes multiple services and infrastructure setup.

---

## **Step 1: Create a GitHub Repository Using GitHub CLI**

To create and manage your repository directly from the terminal, we’ll use GitHub CLI (`gh`). If you don’t have GitHub CLI installed yet, refer to [Part 1: Setup Your Microservice Development Environment](#) for installation instructions.

### **Steps to Create the Repository:**

1. **Log in to GitHub CLI**:
   Open your terminal and run the following command to authenticate with GitHub:

   ```bash
   gh auth login
   ```

   Follow the on-screen instructions to log in to your GitHub account.

2. **Create a New Repository**:
   Now, create a new repository using the following command:

   ```bash
   gh repo create conference-microservices-app --public --source=. --remote=origin
   ```

   This command does the following:
   - **conference-microservices-app**: Name of the repository.
   - `--public`: Makes the repository public (you can make it private if needed).
   - `--source=.`: Indicates that we are creating the repository in the current directory.
   - `--remote=origin`: Adds a remote URL for the repository.

   You should now see a link to your newly created GitHub repository!

---

## **Step 2: Initialize and Organize the Codebase**

Now that the repository is created, we need to initialize a Git repository locally and push the initial code structure. Let’s start by creating a project structure that is well-organized for managing multiple microservices.

### **Create and Organize the Project Structure**

Here’s the structure we’ll use for the **conference-microservices-app** project:

```bash
conference-microservices-app/
│
├── devbox/                 # Devbox environment configuration
│   ├── devbox.json         # Devbox config for tools like Docker, Kubernetes, etc.
│   └── ...
│
├── services/               # Microservices code
│   ├── frontend/           # Frontend service (React, Angular, etc.)
│   ├── c4p-service/        # Call for Papers service (Node.js/Go)
│   ├── agenda-service/     # Agenda management service (Node.js/Go)
│   └── notifications-service/ # Notifications service (Go, Kafka-based)
│
├── infrastructure/         # Infrastructure as Code (IaC) files
│   ├── kubernetes/         # Kubernetes manifests for deploying services
│   ├── terraform/          # Terraform files for cloud infrastructure
│   └── ...
│
├── .gitignore              # Git ignore file to exclude unnecessary files
├── README.md               # Project overview and documentation
└── docker-compose.yml      # Docker Compose file for running microservices locally
```

### **Creating the Directory Structure**

Let’s create the necessary directories and files:

1. Open your terminal and navigate to the root of your project:

   ```bash
   cd conference-microservices-app
   ```

2. Create the directory structure as shown:

   ```bash
   mkdir -p services/{frontend,c4p-service,agenda-service,notifications-service}
   mkdir -p infrastructure/{kubernetes,terraform}
   mkdir devbox
   touch .gitignore README.md docker-compose.yml
   ```

---

## **Step 3: Initialize Git and Add Files**

Now that the directory structure is ready, we’ll initialize Git and commit the initial project setup.

1. **Initialize a Git Repository**:

   ```bash
   git init
   ```

   This will initialize an empty Git repository in the current directory.

2. **Add All Files to Git**:

   ```bash
   git add .
   ```

3. **Commit the Initial Setup**:

   ```bash
   git commit -m "Initial project setup with folder structure"
   ```

---

## **Step 4: Push the Code to GitHub**

Now that we’ve committed the initial setup, it’s time to push the code to the GitHub repository we created earlier.

1. **Push to GitHub**:

   ```bash
   git push origin main
   ```

   This will push your local commits to the remote GitHub repository, and your project will now be available in the `conference-microservices-app` repository on GitHub.

---

## **Step 5: Add a .gitignore File**

A `.gitignore` file is important to prevent unwanted files from being committed to the repository. We’ll exclude files like `node_modules`, `Docker` images, and other local files.

Here’s a basic `.gitignore` file to get started:

```bash
# Node.js
node_modules/
npm-debug.log

# Logs
logs/
*.log

# Docker
*.env
*.log
Dockerfile
.docker/

# Terraform
*.tfstate
*.tfstate.backup

# Kubernetes
.kube/
```

Add this to the `.gitignore` file in the root of your project, then commit and push it:

```bash
git add .gitignore
git commit -m "Add .gitignore to exclude local files"
git push origin main
```

---

## **Step 6: Documentation in README.md**

It’s good practice to add a project description to the `README.md` file. Here’s a basic example:

```markdown
# Conference Microservices Application

This repository contains the codebase for the **Conference Microservices Application**. This app consists of several microservices to manage conferences, including:

- **Frontend**: The user interface for the application.
- **C4P Service**: Handles Call for Papers submissions for speakers.
- **Agenda Service**: Manages the scheduling and display of conference sessions.
- **Notifications Service**: Sends notifications about conference updates.

## Project Structure

```bash
conference-microservices-app/
│
├── devbox/                 # Devbox environment configuration
│   ├── devbox.json         # Devbox config for tools like Docker, Kubernetes, etc.
│   └── ...
│
├── services/               # Microservices code
│   ├── frontend/           # Frontend service (React, Angular, etc.)
│   ├── c4p-service/        # Call for Papers service (Node.js/Go)
│   ├── agenda-service/     # Agenda management service (Node.js/Go)
│   └── notifications-service/ # Notifications service (Go, Kafka-based)
│
├── infrastructure/         # Infrastructure as Code (IaC) files
│   ├── kubernetes/         # Kubernetes manifests for deploying services
│   ├── terraform/          # Terraform files for cloud infrastructure
│   └── ...
│
├── .gitignore              # Git ignore file to exclude unnecessary files
├── README.md               # Project overview and documentation
└── docker-compose.yml      # Docker Compose file for running microservices locally
```

---

## **Conclusion**

With the repository now created and organized, you’ve taken an important step toward managing your microservices project efficiently. The directory structure we’ve outlined will keep the code for each service isolated while maintaining an organized approach to handling infrastructure and environment setup. All future code, services, and configurations should be stored in this repository.

In the next part of the series, we’ll start writing the code for individual microservices, beginning with the **Frontend** and **C4P** services.

Ready to move forward? Head over to [**Part 3: Create Code for Individual Microservices in Repository**](#) and start building the core functionality of the conference application.

---

**GitHub Repository**: [Mastering Microservices with Azure, Docker, Kubernetes, Terraform, and GitHub Actions](https://github.com/cloudikeme/mastering-microservices-with-azure-docker-kubernetes-terraform-github-actions)