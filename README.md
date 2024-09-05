# Medusa Backend Deployment on AWS ECS/Fargate using Terraform & GitHub Actions

This project demonstrates how to deploy the Medusa open-source headless commerce platform backend on AWS ECS/Fargate using Infrastructure as Code (IaC) with Terraform and automates the deployment using GitHub Actions.

https://github.com/user-attachments/assets/6609fd66-e4d7-4f2f-9f40-302fef900918

## Overview

In this project, we:
- Dockerize the Medusa backend.
- Push the Docker image to Amazon ECR (Elastic Container Registry).
- Deploy the containerized backend on AWS ECS/Fargate.
- Automate the deployment process using a Continuous Deployment (CD) pipeline with GitHub Actions.

## Prerequisites

Before you start, make sure you have the following installed:
- [Node.js](https://nodejs.org/)
- [Docker](https://www.docker.com/products/docker-desktop)
- [Terraform](https://www.terraform.io/)
- [AWS CLI](https://aws.amazon.com/cli/)
- [Git](https://git-scm.com/)

Additionally, you will need an AWS account with permissions to:
- Create ECS clusters and services.
- Push Docker images to Amazon ECR.
- Configure IAM roles for task execution.

## Project Setup

### 1. Clone the repository

```bash
git clone https://github.com/Able2002/medusa-ecs-deployment.git
cd medusa-ecs-deployment
```
### 2. Install dependencies
Install the necessary Node.js dependencies for the Medusa backend:

```bash

npm install
```

### 3. Dockerize the Medusa Backend
To dockerize the Medusa backend, a Dockerfile has been provided. It builds the application inside a Docker container with all required dependencies.

Build Docker Image
```bash
docker build -t medusa-backend .
```
### 4. Set up AWS ECS and ECR
You can use Terraform to define your infrastructure as code. The Terraform configuration files (main.tf, ecs.tf, ecr.tf) are provided to create the necessary AWS resources, such as:

VPC, subnets, and security groups.
ECS cluster and Fargate service.
Amazon ECR repository for the Docker image.
Initialize and apply Terraform
```bash

terraform init
terraform apply
```
This will create the infrastructure and output the Amazon ECR repository URL and other resources.

### 5. Push Docker Image to Amazon ECR
Once your infrastructure is set up, push the Docker image to the ECR repository created by Terraform.

```bash

# Log in to ECR
aws ecr get-login-password --region <your-region> | docker login --username AWS --password-stdin <account-id>.dkr.ecr.<your-region>.amazonaws.com

# Tag the Docker image
docker tag medusa-backend:latest <account-id>.dkr.ecr.<your-region>.amazonaws.com/medusa-backend:latest

# Push the Docker image
docker push <account-id>.dkr.ecr.<your-region>.amazonaws.com/medusa-backend:latest

```
### 6. Configure GitHub Actions for CI/CD
A .github/workflows/deploy.yml file is included, which will automate the build and deployment process using GitHub Actions.

Steps in the GitHub Actions Workflow:
Build the Docker image.
Push the image to Amazon ECR.
Update the ECS task definition with the new image.
Deploy the updated ECS task on Fargate.
Setting up GitHub Secrets

Any push to the main branch will trigger the deployment pipeline. You can monitor the GitHub Actions tab to see the progress of the deployment.

### 8. Accessing the Application
Once the deployment is complete, you can access the Medusa backend using the public IP address of your ECS service. Check the ECS console for the public IP and port number.

Useful Terraform Commands
To destroy the infrastructure:


```bash

terraform destroy
Resources
Medusa Documentation
AWS ECS Fargate
Terraform Documentation
GitHub Actions Documentation
```

### License
This project is licensed under the MIT License.

### Author
### Able P Abraham
