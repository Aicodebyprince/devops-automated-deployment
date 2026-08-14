pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t devops-website:v2 .'
            }
        }

        stage('Remove Old Container') {
            steps {
                bat '''
                docker stop devops-container
                docker rm devops-container
                '''
            }
        }

        stage('Run Container') {
            steps {
                bat 'docker run -d -p 9091:80 --name devops-container devops-website:v2'
            }
        }

        stage('Verify Deployment') {
            steps {
                bat 'docker ps'
            }
        }
    }
}