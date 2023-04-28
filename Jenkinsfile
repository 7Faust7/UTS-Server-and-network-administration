pipeline {
    agent any

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
                sh '
