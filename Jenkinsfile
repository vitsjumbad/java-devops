pipeline {
    agent any

    environment {
        IMAGE_NAME = 'springboot-app'
        CONTAINER_NAME = 'springboot-app'
        HOST_PORT = '8082'
        CONTAINER_PORT = '8081'
    }

    stages {
        stage('Build Java App') {
            steps {
                echo '🔧 Building Java app with Maven Wrapper...'
                bat '.\\mvnw clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo '🐳 Building Docker image...'
                bat "docker build -t %IMAGE_NAME% ."
            }
        }

        stage('Stop & Remove Existing Container') {
            steps {
                echo '🧹 Stopping and removing old container (if exists)...'
                bat '''
                docker stop %CONTAINER_NAME% || echo "No container to stop"
                docker rm %CONTAINER_NAME% || echo "No container to remove"
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                echo '🚀 Running new Docker container...'
                bat "docker run -d -p %HOST_PORT%:%CONTAINER_PORT% --name %CONTAINER_NAME% %IMAGE_NAME%"
            }
        }
    }

    post {
        success {
            echo '✅ Deployment successful!'
        }
        failure {
            echo '❌ Deployment failed.'
        }
    }
}

