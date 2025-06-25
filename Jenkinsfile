pipeline {
    agent any

    tools {
        maven 'Maven_3'
    }

    stages {
        stage('Build Java App') {
            steps {
                bat 'mvn clean package'
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
                bat 'docker run -d -p 8082:8081 --name springboot-app springboot-app'
            }
        }
    }
}

