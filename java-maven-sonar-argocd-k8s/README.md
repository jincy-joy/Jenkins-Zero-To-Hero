# Jenkins Pipeline for Java based application using Maven, SonarQube, Argo CD and Kubernetes

![Screenshot 2023-03-28 at 9 38 09 PM](https://user-images.githubusercontent.com/43399466/228301952-abc02ca2-9942-4a67-8293-f76647b6f9d8.png)


This project demonstrates a complete CI/CD pipeline for a Spring Boot application using:

Jenkins (running on AWS EC2)
Maven (for build & test)
SonarQube (for static code analysis, exposed via ngrok)
Docker (to build and push images to Docker Hub)
Kubernetes (using Docker Desktop enabled with k8s)
Argo CD (for GitOps-based continuous deployment)

## Pipeline Workflow

- **Checkout Code** → Pull source code from GitHub  
- **Build & Test** → Compile and package the app into a JAR using Maven  
- **Static Analysis** → Scan the code with SonarQube for quality checks  
- **Build & Push Docker Image** → Build the Docker image and push it to DockerHub  
- **Update Manifests** → Update Kubernetes manifests with the new image tag and push back to GitHub  
- **Argo CD Sync** → Argo CD automatically syncs the changes and deploys the new version to Kubernetes

## Customizations I Made

- Jenkins hosted on AWS EC2 instead of local Docker

- Maven installed via Jenkins tool configuration

- SonarQube exposed with ngrok for external access

- Kubernetes cluster via Docker Desktop with k8s enabled

- Argo CD auto-sync enabled → no manual sync required after deployments.

 ## About

This project is part of my DevOps learning journey.
The base idea came from a training repo(https://github.com/iam-veeramalla/Jenkins-Zero-To-Hero.git), but I customized, integrated, and deployed everything independently.

## Steps Followed in My CI/CD Project

### 1.Set up Jenkins (on EC2):

- Installed Jenkins and configured necessary plugins:

- Git plugin

- Maven Integration plugin

- Pipeline plugin

- Docker Pipeline plugin

### 2.Created a Jenkins pipeline (Multibranch/Declarative):

- Configured the GitHub repository (forked & customized).

- Added a Jenkinsfile to define the pipeline stages.

### 3.Defined pipeline stages:

- Stage 1: Checkout source code from GitHub.

- Stage 2: Build & package Spring Boot app using Maven.

- Stage 3: Run unit tests (via Maven/JUnit).

- Stage 4: Static code analysis using SonarQube (exposed through ngrok).

- Stage 5: Build & push Docker image to Docker Hub.

- Stage 6: Update Kubernetes manifest (deployment.yml) with the new image tag and push changes to GitHub.

- Stage 7: Argo CD automatically syncs from GitHub and deploys to Kubernetes (Docker Desktop).

### 4.Set up Argo CD (locally):

- Installed Argo CD on Docker Desktop Kubernetes.

- Configured GitHub repo (with Kubernetes manifests) as Argo CD’s source.

- Argo CD automatically syncs changes whenever Jenkins pushes updates.

### 5.End-to-End Flow:

Developer pushes code → Jenkins builds, tests, scans, and publishes Docker image → Jenkins updates manifests in GitHub → Argo CD syncs and deploys → Application runs on Kubernetes.
