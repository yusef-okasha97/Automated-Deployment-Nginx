# Automated-Nginx-Deployment

![Automated Photo](automated.gif)

## Table of Contents
- [Project Overview](#Project Overview)
- [CI/CD Pipeline](#cicd-pipeline)
- [Doecker](#Doecker)
- [Ansible](#Ansible)
- [Monitoring with Prometheus and Grafana](#Monitoring with Prometheus and Grafana)
- [Slack Integration for Notifications](#Slack Integration for Notifications)
- [Prerequisites](#Prerequisites)


## Project Overview

This project focuses on implementing a Continuous Integration and Continuous Deployment (CI/CD) pipeline using Jenkins, with integrated monitoring, automated notifications, and containerization to streamline the deployment process. The setup leverages various tools for automation, monitoring, and container management, ensuring smooth and efficient software delivery.

- `index.html`: contains the main project code.


## CI/CD Pipeline

### Jenkins
- Jenkins serves as the core automation server for this CI/CD pipeline. It automates build, test, and deployment processes, ensuring consistent and reliable delivery of application updates.
- The Jenkins server is configured with jobs that handle the entire software lifecycle, from code integration to deployment..

The Jenkins pipeline is designed to automate everything to application deployment. It performs the following steps:
1.  Trigger the change on the GitHub.
2.  Build Docker images.
3.  Run Docker Compose on the VM.
4.  Copy index.html to the Nginx Container.
5.  send the deployment status via Slack.  

- `Note`: you can install Jenkins as a container with all dependencies from my docker hub.
```
docker push yoyo7sniper97/jenkins:latest  
```
 
The Jenkinsfile is located at the root of the project:
- `Jenkinsfile`: Defines the pipeline stages for application deployment.

### Doecker 
- Docker Compose is used to containerize the NGINX server, which serves as a web server for the project. This containerized approach ensures easy deployment, scalability, and consistent environment management for the web server component.
- `docker-compose.yml`: used to create Nginx as a container and Map the local html directory to the container.

### Ansible
 - Ansible is used to automate the installation and configuration of necessary dependencies on the Jenkins agents' VMs.
 - This approach ensures that all agents are consistently set up and reduces manual intervention for agent management.
 - `slave_playbook.yml`: Ansible – Automating instance configuration and Jenkins agent setup

### Monitoring with Prometheus and Grafana
 - Prometheus is set up to collect and store performance metrics from Jenkins, allowing for in-depth monitoring of the pipeline's health and performance.
     - `prometheus.yml`: Defines the targets for prometheus.
 - Grafana visualizes these metrics, providing insightful dashboards that help identify potential bottlenecks and monitor resource usage across the CI/CD pipeline.
 

### Slack Integration for Notifications 
 - The Jenkins setup is integrated with Slack to send notifications about the pipeline status. These notifications include updates on build successes, failures, and deployment completions, allowing teams to stay informed in real time. 

### Prerequisites
- Jenkins for the CI/CD pipeline.
- Docker for containerization.
- Prometheus will collect numeric metrics from services.
- Grafana is used for visualizing the data.
- Slack for sending the deployment notifications.
