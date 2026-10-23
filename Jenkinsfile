pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t cicd-webapp:latest .'
            }
        }

        stage('Deploy Application') {
            steps {
                sh '''
                    docker rm -f cicd-test || true
                    docker run -d --name cicd-test -p 8081:80 cicd-webapp:latest
                '''
            }
        }
    }
}
