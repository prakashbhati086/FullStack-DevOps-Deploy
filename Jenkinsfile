pipeline {
    agent any

    environment {
        IMAGE_NAME = "prakashbhati086/node-auth-app"
        DOCKER_HUB_CREDENTIALS = 'docker-credentials'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/prakashbhati086/FullStack-DevOps-Deploy.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Set Image Tag') {
            steps {
                script {
                    env.IMAGE_TAG = "v${env.BUILD_NUMBER}"
                }
            }
        }

        stage('Docker Build and Push') {
            steps {
                script {
                    echo "📦 Building and pushing image: ${IMAGE_NAME}:${env.IMAGE_TAG}"
                    bat "docker build -t ${IMAGE_NAME}:${env.IMAGE_TAG} ."
                }

                withCredentials([usernamePassword(
                    credentialsId: "${DOCKER_HUB_CREDENTIALS}",
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    bat """
                        echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin
                        docker push ${IMAGE_NAME}:${env.IMAGE_TAG}
                    """
                }
            }
        }
    }

    post {
        success {
            echo "✅ Image pushed: ${IMAGE_NAME}:${env.IMAGE_TAG}"
        }
        failure {
            echo "❌ Docker build or push failed."
        }
    }
}
