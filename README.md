# GitOps Workflow with Custom Git Hooks

This project implements a GitOps workflow using Docker and GitHub Actions to automate the build and deployment of a web application. It also includes a custom setup for Git hooks.

## Description

The application demonstrates GitOps principles, where changes pushed to the `main` branch automatically trigger a workflow to rebuild the Docker image, push it to Docker Hub, and deploy the updated version. Custom Git hooks ensure consistency during local development.

## Technologies Used

- Docker
- GitHub Actions
- Docker Hub
- Custom Git Hooks

## Prerequisites

To replicate or use this project, you need:

- **Docker**: Install it from [here](https://www.docker.com/products/docker-desktop).
- **Docker Hub account**: To store and manage your Docker images.
- **Git**: Install it from [here](https://git-scm.com/).
- **Permissions to configure Git hooks** on your local machine.

## Setting Up Custom Git Hooks

To enable custom Git hooks from the `githooks` folder, follow these steps:

1. **Move the hooks files**:
   Copy the content of the `githooks` folder into the `.git/hooks` directory of your local repository:
   ```bash
   cp -r githooks/* .git/hooks/
   
2. **Verify permissions**:
   Ensure that the hooks have execution permissions:
   ```bash
   chmod +x .git/hooks/*

3. **Test the hooks**:
   Make a commit to verify that the hooks are executed correctly:
   ```bash
   git commit -m "Test custom hooks"
   ```
   If everything is set up properly, you will see the custom hook message in the console.

## GitOps Workflow

1. **Make changes to the code**:
   Push updates to the main branch.

2. **Automated actions**:
   GitHub Actions will automatically build and push the Docker image to Docker Hub.

3. **Update local or production environment**:
   Pull the latest image and redeploy the container.

## Instructions to Run the Project Locally

1. **Clone the Repository**:

   Clone the GitHub repository to your local machine:
   ```bash
   git clone https://github.com/klever1995/githooks.git

2. **Pull the Latest Docker Image**:

   Pull the most recent image from Docker Hub:
   ```bash
   docker pull ksrobalino/gitooks:latest

3. **Pull the Latest Docker Image**:

   Start the application in a Docker container:
   ```bash
   docker run -d -p 8080:80 --name gitops_example ksrobalino/gitooks:latest

4. **Access the application**:

   Open your web browser or use tools like Postman to navigate to:
   ```bash
   http://localhost:8080
   
## Updating the Application

1. **Commit and push changes**:

   ```bash
   git add .
   git commit -m "Update application"
   git push origin main

2. **Pull the latest image**:

   docker pull ksrobalino/gitooks:latest

3. **Replace the current container**:

   Stop and remove the existing container:
   ```bash
   docker rm -f gitops_example
   ```

   Start a new container with the updated image:
   ```bash
   docker run -d -p 8080:80 --name gitops_example ksrobalino/gitooks:latest
   ```

4. **Restart the Container:**

   Stop and remove the current container:
   ```bash
   docker rm -f gitops_example
   ```
    
   Start a new container with the updated image:
   ```bash
   docker run -d -p 8080:80 --name gitops_example ksrobalino/gitops:latest

## Additional Notes

- **Git Hooks Used in This Project**:
  - **Post-commit Hook**: After every commit, this hook checks if the file `index.html` exists in the project and whether it contains the necessary `<html>` and `</html>` tags. If any of these conditions are not met, the commit is blocked and an error message is displayed.
  - **Branch Check Hook**: After every commit, this hook checks the current Git branch. If the commit is made in the `main` branch, it shows a success message. Otherwise, it indicates which branch the commit was made in.

  These Git hooks are designed to automate basic validation and checks during the commit process, ensuring the integrity of the project before changes are pushed.