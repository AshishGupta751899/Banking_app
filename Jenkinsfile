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
        cp /home/ubuntu/Banking_app/.env . || true

        docker stop banking-app || true
        docker rm banking-app || true

        docker run -d \
        --name banking-app \
        --network banking-network \
        --env-file .env \
        -p 5000:5000 \
        banking-app:latest
        '''
       }
      }
    }
}
