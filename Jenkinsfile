pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                echo 'Cloning GitHub repo...'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the application...'
                sh './mvnw clean package'
            }
        }

        stage('Run App') {
            steps {
                echo 'Running Docker container...'
                sh 'docker build -t my-springboot-app .'
                sh 'docker run -d -p 8082:8081 --name springboot-app my-springboot-app'
            }
        }
    }
}

