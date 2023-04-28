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
            sh 'docker build -t redlock-web-2.0 .'
            }
        }
        
        stage('Deploy') {
            steps {
                sh 'docker stop redlock-web-container || true'
                sh 'docker rm redlock-web-container || true'
                sh 'docker run -d --name redlock-web-container -p 7077:80 --link redlock-db-container:mysql redlock-web-2.0'
            }
        }
    }
}

