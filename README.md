# Azure Python DevOps CI/CD Pipeline

An end-to-end DevOps project that automates the build, testing, containerization, and deployment of a FastAPI application on Microsoft Azure using GitHub Actions, Docker, and Terraform.

## Project Overview

This project demonstrates a complete CI/CD pipeline following DevOps best practices. Every push to the main branch automatically:

- Runs unit tests using pytest
- Builds a Docker image
- Pushes the image to Azure Container Registry (ACR)
- Deploys the latest version using Terraform
- Hosts the application on Azure Container Instance (ACI)

Additionally, the same application was deployed to Azure App Service (Linux F1 Free Tier) for a permanently free hosting option.

## Architecture

```text
GitHub
    │
    ▼
GitHub Actions
    │
    ├── Run Unit Tests (pytest)
    ├── Build Docker Image
    ├── Push Image to Azure Container Registry
    └── Terraform Apply
            │
            ▼
Azure Container Registry
            │
            ▼
Azure Container Instance (ACI)

(Optional)
            │
            ▼
Azure App Service (Linux F1)
```

## Tech Stack

- Python 3.11
- FastAPI
- Pytest
- Docker
- GitHub Actions
- Terraform
- Microsoft Azure
- Azure Container Registry (ACR)
- Azure Container Instance (ACI)
- Azure App Service (Linux F1)
- Azure Storage Account (Terraform Remote State)

## Project Structure

```text
azure-python-devops/
├── .github/
│   └── workflows/
│       └── deploy.yml
├── app/
│   ├── main.py
│   ├── requirements.txt
│   ├── Dockerfile
│   └── tests/
│       └── test_main.py
├── infra/
│   ├── main.tf
│   ├── variables.tf
│   ├── outputs.tf
│   └── .terraform.lock.hcl
├── .gitignore
├── LICENSE
└── README.md
```

## CI/CD Pipeline

The GitHub Actions workflow performs the following:

- Checkout repository
- Install Python dependencies
- Execute unit tests
- Build Docker image
- Push image to Azure Container Registry
- Initialize Terraform
- Validate Terraform configuration
- Deploy infrastructure and application to Azure

## Infrastructure as Code

Terraform provisions:

- Azure Resource Group
- Azure Container Registry
- Azure Container Instance
- Remote Terraform State using Azure Storage Account

The Terraform state is stored remotely in Azure Storage for consistent deployments across environments.

## Application Endpoints

Azure Container Instance
http://azpydevops-app.centralindia.azurecontainer.io:8000/

Health Check
http://azpydevops-app.centralindia.azurecontainer.io:8000/health

Azure App Service (Linux F1)
https://azpydevops-webapp.azurewebsites.net/

## GitHub Secrets Required

The workflow requires the following GitHub Secrets:

| Secret | Description |
|---------|-------------|
| AZURE_CREDENTIALS | Azure Service Principal credentials |
| REGISTRY_USERNAME | Azure Container Registry username |
| REGISTRY_PASSWORD | Azure Container Registry password |

## Key Features

- Automated CI/CD pipeline
- Infrastructure as Code with Terraform
- Remote Terraform state in Azure Storage
- Dockerized FastAPI application
- Automated testing using Pytest
- Azure Container Registry integration
- Azure Container Instance deployment
- Azure App Service (Linux F1) deployment
- GitHub Actions automation

## Challenges Faced

During development, I resolved several real-world DevOps issues, including:

- Terraform state conflicts when Azure resources already existed
- Migrating Terraform state from local storage to Azure Storage backend
- Configuring GitHub Actions authentication with Azure Service Principal
- Managing Azure Container Registry authentication
- Deploying Docker containers to Azure App Service (Linux F1)
- Configuring application ports and container startup settings
- Handling Git version control and Terraform state files correctly

## Learning Outcomes

This project strengthened my understanding of:

- CI/CD pipeline implementation
- GitHub Actions workflows
- Docker containerization
- Infrastructure as Code (Terraform)
- Azure cloud services
- Remote Terraform state management
- Azure authentication and role-based access control (RBAC)
- End-to-end application deployment automation

## Future Improvements

- Add Terraform Plan approval before deployment
- Integrate SonarQube code quality analysis
- Add Trivy container image scanning
- Implement Blue-Green deployment strategy
- Deploy to Azure Kubernetes Service (AKS)
- Add monitoring using Azure Monitor and Application Insights

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/raimadb/azure-python-devops.git
cd azure-python-devops```

### 2. Configure GitHub Secrets

Add the following repository secrets:

- AZURE_CREDENTIALS
- REGISTRY_USERNAME
- REGISTRY_PASSWORD

### 3. Push changes

Every push to the main branch automatically:

- Runs unit tests
- Builds the Docker image
- Pushes the image to Azure Container Registry
- Deploys the latest version using Terraform

## Author
Raima Deb Barma
