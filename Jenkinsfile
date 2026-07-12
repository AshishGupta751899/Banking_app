pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t banking_app-app:latest .'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker stop banking-app || true
                docker rm banking-app || true

                docker run -d \
                  --name banking-app \
                  --network bridge \
                  --env-file .env \
                  -p 5000:5000 \
                  banking_app-app:latest
                '''
            }
        }
    }
}pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build & Deploy') {
            steps {
                sh '''
                docker compose down || true
                docker compose up -d --build
                '''
            }
        }
    }
}
