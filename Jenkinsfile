pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/Aicodebyprince/devops-automated-deployment.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t devops-website:v2 .'
            }
        }

        stage('Remove Old Container') {
            steps {
                bat '''
                docker stop devops-container || exit 0
                docker rm devops-container || exit 0
                '''
            }
        }

        stage('Run Container') {
            steps {
                bat 'docker run -d -p 9090:80 --name devops-container devops-website:v2'
            }
        }

        stage('Verify Deployment') {
            steps {
                bat 'docker ps'
            }
        }
    }
}