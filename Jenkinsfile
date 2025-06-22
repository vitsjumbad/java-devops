
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                bat './mvnw.cmd clean package'
            }
        }

        stage('Run') {
            steps {
                bat 'docker build -t springboot-app .'
                bat 'docker run -d -p 8082:8081 --name springboot-app springboot-app'
            }
        }
    }
}

