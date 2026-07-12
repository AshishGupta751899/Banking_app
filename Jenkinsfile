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
                sh 'docker build -t banking-app:latest .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                docker stop banking-app || true
                docker rm banking-app || true
                '''
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker run -d \
                --name banking-app \
                -p 5000:5000 \
                banking-app:latest
                '''
            }
        }
    }
}
