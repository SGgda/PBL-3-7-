pipeline {
    agent any

    environment {
        DOCKER_HUB_USER = "your_dockerhub_username" // Change this
        IMAGE_NAME = "pbl-app"
        IMAGE_TAG = "latest"
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/your-username/your-repo.git' // Change this
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${DOCKER_HUB_USER}/${IMAGE_NAME}:${IMAGE_TAG}")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('', 'docker-hub-credentials-id') { // Add credentials in Jenkins
                        dockerImage.push()
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    // Replaces the placeholder in the yaml file
                    sh "sed -i 's/\${DOCKER_HUB_USER}/${DOCKER_HUB_USER}/g' k8s/deployment.yaml"
                    
                    // Apply the manifests
                    sh "kubectl apply -f k8s/deployment.yaml"
                    sh "kubectl apply -f k8s/service.yaml"
                }
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully!"
        }
        failure {
            echo "Pipeline failed. Check the logs."
        }
    }
}
