# **Mastering Microservices: Setup Your Development Environment with Devbox**

Welcome to **Part 1 of the Mastering Microservices Series**: Setting up your microservice development environment. In this tutorial, we'll introduce you to the environment you’ll need to build and run microservices locally. To make the setup process simple and consistent, I (the author) have created a **pre-configured Devbox environment** specifically for this project. By using Devbox, you can skip manual installations and configurations, ensuring that all necessary tools are available and correctly configured.

This environment is ideal for those working on Windows, macOS, or Linux and want to hit the ground running with a fully-equipped microservices development setup.

---

## **Why Use Devbox for This Project?**

Devbox is a tool that allows you to create isolated, reproducible development environments. Instead of manually installing each tool (like Docker, Kubernetes, Terraform, Node.js, Go, etc.), you can use Devbox to spin up a development environment pre-configured with everything you need for this project.

I’ve tailored the Devbox environment specifically for the **Mastering Microservices** series, so you won’t have to worry about dependency conflicts or configuration issues. This setup ensures a consistent environment for all developers working on the project.

---

## **Steps to Use the Pre-Configured Devbox Environment**

Follow these steps to set up and activate the Devbox environment for your local microservices development:

---

### **Step 1: Clone the GitHub Repository**

To begin, clone the GitHub repository where the microservices project and Devbox environment are hosted.

1. Open your terminal and run the following command to clone the repository:

   ```bash
   git clone https://github.com/cloudikeme/mastering-microservices-with-azure-docker-kubernetes-terraform-github-actions.git
   ```

2. Navigate to the root folder of the project:

   ```bash
   cd mastering-microservices-with-azure-docker-kubernetes-terraform-github-actions
   ```

---

### **Step 2: Install Devbox**

If you don’t already have Devbox installed on your local machine, here’s how to install it:

1. **For Linux/macOS:**

   ```bash
   curl -fsSL https://get.jetpack.io/devbox | bash
   ```

2. **For Windows:**
   If you are on Windows, you can install Devbox via WSL (Windows Subsystem for Linux) following the same steps as for Linux.

3. **Verify Installation:**

   After installation, confirm that Devbox is installed by running:

   ```bash
   devbox --version
   ```

You can also refer to the official [Devbox installation guide](https://www.jetpack.io/devbox/docs/) if you encounter any issues.

---

### **Step 3: Activate the Pre-Configured Devbox Environment**

The repository includes a Devbox configuration file (`devbox.json`) that automatically sets up the required tools for the project. To activate the development environment:

1. Change into the Devbox folder inside the project:

   ```bash
   cd devbox
   ```

2. Activate the Devbox shell:

   ```bash
   devbox shell
   ```

This command will activate a development environment with all the tools needed for the microservices project, including:

- **Docker**: For containerizing microservices.
- **kubectl**: To interact with Kubernetes clusters.
- **Terraform**: For infrastructure as code.
- **Node.js and npm**: For JavaScript microservices and package management.
- **Go**: For building Go-based microservices.
- **Git and GitHub CLI**: For version control and interacting with GitHub.
- **kind**: For running a local Kubernetes cluster inside Docker.

---

## **Tools Pre-Configured in the Devbox Environment**

Here’s a quick overview of the tools that come pre-installed in this environment:

1. **Docker**: Used for containerizing and running your microservices.
2. **kubectl**: Kubernetes command-line tool for managing your local or cloud Kubernetes clusters.
3. **Terraform**: Enables you to define and provision infrastructure using code.
4. **Node.js & npm**: Node.js runtime and npm for managing JavaScript dependencies.
5. **Go**: Go programming language, commonly used for building efficient microservices.
6. **Git**: Version control system to track changes in your code.
7. **GitHub CLI (gh)**: Makes working with GitHub from the command line easier.
8. **kind**: Lets you run Kubernetes clusters locally in Docker for easy testing and development.

---

## **Step 4: Verify the Setup**

After activating the Devbox shell, verify that all the tools are correctly installed and available in your environment:

- **Check Docker**:

   ```bash
   docker --version
   ```

- **Check kubectl**:

   ```bash
   kubectl version --client
   ```

- **Check Terraform**:

   ```bash
   terraform --version
   ```

- **Check Node.js**:

   ```bash
   node --version
   ```

- **Check Go**:

   ```bash
   go version
   ```

- **Check Git**:

   ```bash
   git --version
   ```

You should see the version information for each tool, indicating that your Devbox environment is properly set up.

---

## **Why I Created a Pre-Configured Devbox Environment**

When building microservices, having a consistent and ready-to-use development environment is critical. By pre-configuring the Devbox environment, I’ve ensured that every developer working on this project has access to the same tools, configured in the same way. This avoids issues like "it works on my machine" and accelerates the onboarding process for new developers.

**Benefits of Using Devbox**:
- **Consistency**: Everyone on the project uses the same versions of tools and libraries.
- **Isolation**: The development environment is isolated from your local machine, preventing conflicts with other projects.
- **Reproducibility**: You can recreate the environment on any machine by simply cloning the repository and activating Devbox.
- **Speed**: Get started faster with all tools pre-configured and ready to use.

---

## **Next Steps**

Once your Devbox environment is activated and verified, you can proceed with developing and running the microservices. In the next part of this series, we’ll set up Git repositories and organize the code for the microservices.

Continue with [**Part 2: Create a Repository from Linux Terminal Using Git and GitHub CLI**](#) to begin managing your microservices codebase with Git and GitHub.

---

**GitHub Repository**: [Mastering Microservices with Azure, Docker, Kubernetes, Terraform, and GitHub Actions](https://github.com/cloudikeme/mastering-microservices-with-azure-docker-kubernetes-terraform-github-actions)

---

With the Devbox environment ready, you’re equipped to move forward in this series with ease. By using the pre-configured tools, you can focus on building and deploying microservices without worrying about the complexities of local setup.