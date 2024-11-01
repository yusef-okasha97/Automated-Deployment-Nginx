# Automated-Deployment-Pipeline-with-Jenkins-and-Docker

![Automated Photo](automated.gif)

This repository contains the infrastructure and deployment setup for the **To-Do App**, a simple task management application. The project is built with a comprehensive DevOps pipeline using Terraform, Ansible, Jenkins, Kubernetes, and ArgoCD for infrastructure and continuous delivery.

## Table of Contents
- [Overview](#overview)
- [CI/CD Pipeline](#cicd-pipeline)
- [License](#license)

## Overview

This project automates the provisioning of ifrastructure and the deployment of the **To-Do App**. The pipeline manages the entire lifecycle from infrastructure creation on AWS (using Terraform) to application deployment on Kubernetes using Helm and ArgoCD.


## CI/CD Pipeline

### Jenkins
The Jenkins pipeline is designed to automate the entire process from infrastructure provisioning to application deployment. It performs the following steps:
1. Provision infrastructure using Terraform.
2. Run Ansible playbooks to configure instances.
3. Build and push Docker images (if needed).
4. Deploy the application to Kubernetes using Helm and ArgoCD.

The Jenkinsfile is located at the root of the project:
- `Jenkinsfile`: Defines the pipeline stages for infrastructure provisioning and application deployment.


### Ansible

## Getting Started

### Prerequisites
- Jenkins for the CI/CD pipeline
- Docker for containerization

