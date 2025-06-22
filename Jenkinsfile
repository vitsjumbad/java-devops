pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/vitsjumbad/java-devops.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t springboot-app .'
            }
        }

        stage('Stop & Remove Existing Container') {
            steps {
                bat '''
                docker stop springboot-app || exit 0
                docker rm springboot-app || exit 0
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                bat 'docker run -d -p 8082:8080 --name springboot-app springboot-app'
            }
        }
    }
}
