## Mastering Microservices: Setting Up Your Development Environment with Devbox

Welcome to **Part 1 of the Mastering Microservices Series!** In this tutorial, I'll guide you through setting up your microservice development environment. I've created a **pre-configured Devbox environment** to streamline the process. With Devbox, you can skip manual installations and configurations — all the tools you need will be ready to use.

This environment is a perfect fit for Windows, macOS, or Linux users who want a fully equipped setup to start building microservices right away.

---

## Why Choose Devbox for This Project?

Devbox allows you to create isolated, reproducible development environments. Instead of manually installing tools like Docker, Kubernetes, Terraform, Node.js, and Go, you can use Devbox to spin up a pre-configured environment tailored specifically for this project.

I've customized this Devbox environment for the **Mastering Microservices Series**, so you won't encounter dependency conflicts or configuration issues. This ensures a consistent experience for all developers contributing to the project. 

---

## Setting Up Your Pre-Configured Devbox Environment

Follow these steps to prepare your local microservices development environment with Devbox:

---

### Step 1: Clone the GitHub Repository

First, clone the GitHub repository containing the project and its Devbox environment:

1. Open your terminal and run this command:

   ```bash
   git clone https://github.com/cloudikeme/mastering-microservices-with-azure-docker-kubernetes-terraform-github-actions.git
   ```

2. Navigate to the project's root folder:

   ```bash
   cd mastering-microservices-with-azure-docker-kubernetes-terraform-github-actions
   ```

---

### Step 2: Install Devbox

If you haven't installed Devbox on your system, follow these instructions:

1. **For Linux/macOS:**

   ```bash
   curl -fsSL https://get.jetpack.io/devbox | bash
   ```

2. **For Windows:**
   Install Devbox through WSL (Windows Subsystem for Linux) using the same steps as for Linux.  Find WSL-specific instructions in the [Devbox WSL documentation](https://www.jetpack.io/devbox/docs/wsl/).

3. **Verification:**

   After installation, run this command to verify Devbox is ready:

   ```bash
   devbox --version
   ```

   Your terminal should display the installed Devbox version.

Encounter installation issues? Refer to the official [Devbox installation guide](https://www.jetpack.io/devbox/docs/).

---

### Step 3: Activate Your Devbox Environment

The repository includes a `devbox.json` configuration file. This file automatically sets up the tools you'll need. Let's activate the environment:

1. Navigate to the Devbox folder:

   ```bash
   cd devbox
   ```

2. Activate the Devbox shell:

   ```bash
   devbox shell
   ```

   Devbox will now download and install the required tools. A change in your terminal prompt will indicate you're working within the Devbox environment.

---

## Tools in Your Devbox Environment

Here's a summary of the pre-installed tools in your Devbox environment:

1. **Docker:** Use Docker to containerize and run your microservices.
2. **kubectl:** Manage your Kubernetes clusters (local or cloud-based) with this command-line tool. 
3. **Terraform:** Define and manage your infrastructure as code.
4. **Node.js & npm:** Utilize the Node.js runtime and npm for managing JavaScript dependencies.
5. **Go:** Build efficient microservices with the Go programming language.
6. **Git:** This version control system helps you track changes in your code.
7. **GitHub CLI (gh):** Interact with GitHub seamlessly, right from your command line.
8. **kind:** Run local Kubernetes clusters within Docker for easy testing and development.

---

## Step 4: Verify Your Setup

After activating the Devbox shell, verify the correct installation of your tools:

- **Check Docker:**

   ```bash
   docker --version
   ```
   <img src="docker-version.png" alt="docker --version output" width="600"/> 

- **Check kubectl:**

   ```bash
   kubectl version --client 
   ```
   <img src="kubectl-version.png" alt="kubectl version --client output" width="600"/> 

- **Check Terraform:**

   ```bash
   terraform --version
   ```
    <img src="terraform-version.png" alt="terraform --version output" width="600"/> 

- **Check Node.js:**

   ```bash
   node --version
   ```
   <img src="node-version.png" alt="node --version output" width="600"/> 

- **Check Go:**

   ```bash
   go version
   ```
   <img src="go-version.png" alt="go version output" width="600"/> 

- **Check Git:**

   ```bash
   git --version
   ```
   <img src="git-version.png" alt="git --version output" width="600"/> 

The output should show the version information for each tool, confirming your Devbox environment is properly set up.

---
## Manual Installation (Optional)

Though Devbox simplifies the process, you can choose to install the tools manually:

<details>
  <summary>Manual Installation Instructions</summary>

If you opt for manual installation, refer to these guides for each tool and ensure compatibility with your operating system:

  * **Docker:** [https://docs.docker.com/get-docker/](https://docs.docker.com/get-docker/)
  * **kubectl:** [https://kubernetes.io/docs/tasks/tools/install-kubectl/](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
  * **Terraform:** [https://learn.hashicorp.com/tutorials/terraform/install-cli](https://learn.hashicorp.com/tutorials/terraform/install-cli)
  * **Node.js and npm:** [https://nodejs.org/](https://nodejs.org/)
  * **Go:** [https://go.dev/doc/install](https://go.dev/doc/install)
  * **Git:** [https://git-scm.com/downloads](https://git-scm.com/downloads)
  * **GitHub CLI:** [https://cli.github.com/](https://cli.github.com/)
  * **kind:** [https://kind.sigs.k8s.io/docs/user/quick-start/](https://kind.sigs.k8s.io/docs/user/quick-start/) 
</details>

---

## Troubleshooting Devbox

If you encounter problems, here are some Devbox troubleshooting tips:

* **Keep Devbox Updated:** Run `devbox update` to download the latest version.
* **Network Check:**  Ensure a stable internet connection for Devbox to download and install tools. 
* **Review the Logs:**  Devbox logs can provide detailed error messages if installations fail.
* **Clean Reinstall:** If you suspect problems, use `devbox rm` to remove the environment. Then, recreate it with `devbox shell`.

Find additional help in the official [Devbox documentation](https://www.jetpack.io/devbox/docs/).

---

## What's Next?

You've set up your Devbox environment — now you're ready to build microservices! In Part 2, we'll establish Git repositories and structure our microservices codebase.

Head to [**Part 2: Create a Repository from Linux Terminal Using Git and GitHub CLI**](#) to begin managing your code with Git and GitHub.

---

**GitHub Repository:** Find all the code for this series in the [Mastering Microservices with Azure, Docker, Kubernetes, Terraform, and GitHub Actions](https://github.com/cloudikeme/mastering-microservices-with-azure-docker-kubernetes-terraform-github-actions) repository.

---

You're off to a great start! This setup frees you to focus on the exciting part — building and deploying microservices. I'll see you in Part 2! 
