pipeline {
    agent any

    environment {
        DOCKER = 'C:\\Users\\princ\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe'
    }

    stages {

        stage('Check Docker') {
            steps {
                bat "\"%DOCKER%\" --version"
            }
        }

        stage('Build Docker Image') {
            steps {
                bat "\"%DOCKER%\" build -t devops-website:v2 ."
            }
        }

        stage('Remove Old Container') {
            steps {
                bat '''
                "%DOCKER%" stop devops-container || exit /b 0
                "%DOCKER%" rm devops-container || exit /b 0
                '''
            }
        }

        stage('Run Container') {
            steps {
                bat "\"%DOCKER%\" run -d -p 9091:80 --name devops-container devops-website:v2"
            }
        }

        stage('Verify Deployment') {
            steps {
                bat "\"%DOCKER%\" ps"
            }
        }

        stage('Verify Image') {
            steps {
                bat "\"%DOCKER%\" images"
            }
        }
    }

    post {
        success {
            echo 'Deployment Successful!'
        }

        failure {
            echo 'Deployment Failed!'
        }
    }
}