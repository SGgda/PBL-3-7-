# CI/CD Pipeline: Docker + Jenkins + Kubernetes

This project demonstrates a simple CI/CD pipeline implementation for a DevOps assignment.

## Components
1. **Application**: A simple, beautiful HTML page (`index.html`).
2. **Dockerization**: A `Dockerfile` using Nginx to serve the static page.
3. **Orchestration**: Kubernetes manifests (`k8s/`) for deploying the app with 2 replicas and a LoadBalancer service.
4. **CI/CD Pipeline**: A `Jenkinsfile` defining the automation stages.

## Pipeline Stages
1. **Checkout**: Pulls the latest code from the repository.
2. **Build Docker Image**: Builds the container image from the Dockerfile.
3. **Push to Docker Hub**: Uploads the image to a container registry.
4. **Deploy to Kubernetes**: Uses `kubectl` to apply the deployment and service manifests to the cluster.

## Prerequisites
- **Jenkins** with Docker and Kubernetes plugins installed.
- **Docker Hub** account.
- **Kubernetes Cluster** (Minikube, K3s, or Managed K8s).
- **Credentials**: Configure Docker Hub credentials in Jenkins with the ID `docker-hub-credentials-id`.
