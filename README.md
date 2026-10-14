# 🚀 Automated Docker Deployment Using GitHub Actions, Amazon ECR & EC2

## 📌 Project Overview

This project demonstrates an automated CI/CD pipeline using **GitHub Actions, Docker, Amazon Elastic Container Registry (ECR), and Amazon EC2**.

Whenever code is pushed to the `main` branch, GitHub Actions automatically builds a Docker image and pushes it to a private Amazon ECR repository. The image can then be deployed to an EC2 instance to run the application.

The goal is to automate application deployment, reduce manual effort, and understand how CI/CD pipelines work in a real-world DevOps environment.

## 🏗️ Architecture

```text
        Developer
            |
            | Git Push
            v
     GitHub Repository
            |
            v
      GitHub Actions
            |
            v
       Docker Build
            |
            v
      Amazon ECR
      (Private Repo)
            |
            v
        Amazon EC2
            |
            v
    Docker Container
            |
            v
      Web Application
```

## 🛠️ Technologies Used

| Technology     | Purpose                        |
| -------------- | ------------------------------ |
| Git & GitHub   | Source code management         |
| GitHub Actions | CI/CD automation               |
| Docker         | Containerization               |
| Amazon ECR     | Private Docker image registry  |
| Amazon EC2     | Application hosting            |
| AWS IAM        | Access control and permissions |
| YAML           | Pipeline configuration         |
| Linux          | Server administration          |

## ⚙️ Project Workflow

1. Developer pushes code to the GitHub repository.
2. GitHub Actions triggers the workflow on a push to the `main` branch.
3. The runner checks out the latest source code.
4. Docker builds an image using the application's Dockerfile.
5. GitHub Actions authenticates with AWS.
6. The Docker image is pushed to the private Amazon ECR repository.
7. The image can be pulled onto an EC2 instance for deployment.
8. The application runs inside a Docker container.

## 🔐 AWS Configuration

The project uses the following AWS services:

### 1. Amazon ECR

* Created a private ECR repository named `gitaction`.
* Stores Docker images securely.
* Provides a central registry for application images.

### 2. AWS IAM

* Configured IAM permissions for accessing Amazon ECR.
* Used AWS authentication in the GitHub Actions workflow.
* Followed the principle of least privilege wherever applicable.

### 3. Amazon EC2

* Uses an EC2 instance running Amazon Linux 2023.
* Docker must be installed and running.
* The instance requires permission to pull images from the private ECR repository.

## 🔄 CI/CD Automation

The GitHub Actions workflow is configured to trigger when code is pushed to the `main` branch.

Example workflow trigger:

```yaml
name: Build and Push Docker Image to Amazon ECR

on:
  push:
    branches:
      - main
```

The complete workflow can include the following stages:

* Checkout source code
* Authenticate with AWS
* Log in to Amazon ECR
* Build the Docker image
* Tag the image
* Push the image to the private ECR repository

## 📂 Project Structure

```text
gitaction/
│
├── .github/
│   └── workflows/
│       └── deploy.yml
│
├── Dockerfile
├── index.html
└── README.md
```

*Note: Update the file names in this structure to match your actual repository.*

## 💻 Useful Commands

### Build Docker Image

```bash
docker build -t gitaction .
```

### View Docker Images

```bash
docker images
```

### Authenticate Docker with Amazon ECR

```bash
aws ecr get-login-password --region YOUR_AWS_REGION | docker login --username AWS --password-stdin YOUR_AWS_ACCOUNT_ID.dkr.ecr.YOUR_AWS_REGION.amazonaws.com
```

### Tag Docker Image

```bash
docker tag gitaction:latest YOUR_AWS_ACCOUNT_ID.dkr.ecr.YOUR_AWS_REGION.amazonaws.com/gitaction:latest
```

### Push Image to Amazon ECR

```bash
docker push YOUR_AWS_ACCOUNT_ID.dkr.ecr.YOUR_AWS_REGION.amazonaws.com/gitaction:latest
```

### Pull Image on EC2

```bash
docker pull YOUR_AWS_ACCOUNT_ID.dkr.ecr.YOUR_AWS_REGION.amazonaws.com/gitaction:latest
```

Replace the placeholders with your actual AWS account ID and region.

## 🔒 Security Best Practices

* Store sensitive credentials in GitHub Actions Secrets or use GitHub OIDC with an appropriately configured IAM role.
* Never hardcode AWS access keys or private SSH keys in source code.
* Use IAM policies with only the permissions required.
* Keep the ECR repository private.
* Restrict EC2 security group access to the required ports.
* Use unique Docker image tags for traceability.

## 🎯 Key Learning Outcomes

* Understanding CI/CD pipeline automation.
* Integrating GitHub Actions with AWS.
* Building Docker images automatically.
* Pushing container images to Amazon ECR.
* Understanding IAM roles and AWS permissions.
* Working with Amazon EC2 and Amazon Linux.
* Learning container deployment and troubleshooting.

## 👨‍💻 Author

**Raj Kushwaha**

Aspiring DevOps Engineer

Skills: AWS | Linux | Docker | Git | GitHub Actions | Jenkins | Kubernetes | Terraform

GitHub: [rajkushwaha01](https://github.com/rajkushwaha01)

LinkedIn: [Connect with me](https://www.linkedin.com/in/raj-kushwahaa/)

---

⭐ If you find this project useful, feel free to explore the repository!
