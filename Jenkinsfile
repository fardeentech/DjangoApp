pipeline {
    agent any 

    environment {
        DOCKER_IMAGE = "https://hub.docker.com/repository/docker/pathan003/djangoapp/general"
    }

    stages {
        stage('Clone Repository') {
            steps {
                echo "Cloning repository from GitHub..."
                git branch: 'main', url: 'https://github.com/fardeentech/DjangoApp.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Building Docker image..."
                sh 'docker build -t ${DOCKER_IMAGE} .'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                echo "Logging in to Docker Hub..."
                withCredentials([string(credentialsId: 'docker-hub-password', variable: 'DOCKER_PASSWORD')]) {
                    sh 'echo "$DOCKER_PASSWORD" | docker login -u "gunjanpandya" --password-stdin'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                echo "Pushing Docker image to Docker Hub..."
                sh 'docker push ${DOCKER_IMAGE}'
            }
        }
    }

    post {
        success {
            echo "✅ CI/CD Pipeline completed successfully! 🚀"
        }
        failure {
            echo "❌ Pipeline failed! Check the logs for errors."
        }
    }
}