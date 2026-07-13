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
                sh '''
                docker build -t banking-app:latest .
                '''
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
                  --link banking-mysql:mysql \
                  --env-file .env \
                  -p 5000:5000 \
                  banking-app:latest
                '''
            }
        }
    }
}
