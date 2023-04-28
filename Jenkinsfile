pipeline {
    agent any

     environment {
        DOCKER_PATH = 'C:\Program Files\Docker\Docker\resources\bin\'
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Check Docker') {
            steps {
                echo "DOCKER_HOST: ${env.DOCKER_HOST}"
                sh "docker version"
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
