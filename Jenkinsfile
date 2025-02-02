pipeline {
    agent any

    environment {
        DOCKER_REGISTRY = 'docker.io/chaitrashreekd'  // Docker Hub registry URL (use your username)
        BACKEND_IMAGE = 'backend'                      // Backend Docker image name
        FRONTEND_IMAGE = 'frontend'                    // Frontend Docker image name
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the repository code from GitHub
                git 'https://github.com/chaitrashreekd/final-project.git'  // Replace with your actual GitHub repo URL
            }
        }

        stage('Build Backend Docker Image') {
            steps {
                script {
                    // Build backend Docker image
                    sh 'docker build -t $DOCKER_REGISTRY/$BACKEND_IMAGE ./backend'
                }
            }
        }

        stage('Build Frontend Docker Image') {
            steps {
                script {
                    // Build frontend Docker image
                    sh 'docker build -t $DOCKER_REGISTRY/$FRONTEND_IMAGE ./frontend'
                }
            }
        }

        stage('Push Docker Images') {
            steps {
                script {
                    // Login to Docker Hub using Jenkins credentials
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        sh "echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin"
                    }
                    // Push images to Docker Hub
                    sh 'docker push $DOCKER_REGISTRY/$BACKEND_IMAGE'
                    sh 'docker push $DOCKER_REGISTRY/$FRONTEND_IMAGE'
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the backend and frontend images...'
            }
        }
    }

    post {
        success {
            echo 'Build and deployment successful!'
        }
        failure {
            echo 'Build failed.'
}
}
}
