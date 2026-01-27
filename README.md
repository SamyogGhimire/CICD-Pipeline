# CICD Pipeline Project

## Prerequisites:
- Jenkins
- Git/GitHub
- Maven
- Docker
- ArgoCD (GitOps CD Tool)
- Kubernetes (Minikube Local Cluster)

## Architecture
![Architecture](./images/Architecture.png)

## Description
This project demonstrates a complete CI/CD pipeline for a Java Spring Boot application using Jenkins for Continuous Integration (CI) and GitOps with ArgoCD for Continuous Delivery (CD).

The application source code resides in a GitHub repository, while Kubernetes deployment manifests are maintained in a separate GitOps repository.

When a developer pushes code:
- A GitHub webhook triggers Jenkins.
- Jenkins builds and tests the application using Maven.
- Jenkins builds and pushes a Docker image to Docker Hub.
- Jenkins updates the Kubernetes deployment manifest with the new image tag and commits it back to Git.
- ArgoCD automatically syncs the updated manifests and deploys the new version to a Minikube cluster.

This setup ensures Git remains the single source of truth and enables automated, auditable, and rollback-friendly deployments.



## CI/CD Pipeline Flow

### 1. Code Commit  
Developer pushes code changes to the GitHub repository.

---

### 2. GitHub Webhook Trigger  
A GitHub webhook immediately notifies Jenkins about the new commit, avoiding continuous polling.

---

### 3. Jenkins CI Pipeline  
Jenkins starts the CI pipeline defined in the declarative `Jenkinsfile`.

---

### 4. Maven Build & Test  
Jenkins runs Maven to:  
- Compile the Spring Boot application  
- Resolve dependencies  
- Execute unit tests  
If the build or tests fail, the pipeline stops.

---

### 5. Docker Build & Push  
Jenkins:  
- Builds a Docker image for the application  
- Tags it with the Jenkins build number  
- Pushes the image to Docker Hub

---

### 6. Kubernetes Manifest Update (GitOps)
  
Jenkins updates the Kubernetes deployment manifest with the new Docker image tag and commits the change back to Git, keeping Git as the single source of truth.

---

### 7. ArgoCD Sync  
ArgoCD detects the updated manifest in Git and automatically syncs the changes to the Kubernetes cluster.

---

### 8. Deployment to Kubernetes  
The new application version is rolled out to Minikube automatically using Kubernetes rolling updates.

---

### 9. Audit & Rollback  
All deployment changes are tracked in Git.  
If an issue occurs, rolling back is as simple as reverting a Git commit, and ArgoCD will automatically apply the previous state.

---

## Output Screenshots:

### Jenkins Pipeline (Successful Build)
![Jenkins Pipeline(Successful Build)](./images/Jenkins.png)

### ArgoCD Application (Successful Sync)
![ArgoCD Application](./images/ArgoCD.png)

### Deployed Application (Minikube IP)
![Deployed Application (Minikube IP)](./images/deployed.png)

---

## Key Learnings

- End-to-end CI/CD automation  
- GitOps with ArgoCD  
- GitHub webhook–triggered Jenkins builds  
- Docker image versioning best practices  
- Automated Kubernetes rollouts  
- Git-based audit & rollback  

---

## Docker Image

The latest Docker image for this project is available on Docker Hub:

```bash
docker pull samyogg/java-cicd-pipeline:35
```

You can run it locally with:
```bash
docker run -p 8080:8080 samyogg/java-cicd-pipeline:35

```
