pipeline {
    agent any

    environment {
        DOCKER = 'C:\\Users\\princ\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe'
        SSH = 'C:\\Windows\\System32\\OpenSSH\\ssh.exe'
        SSH_KEY = 'C:\\JenkinsKeys\\devops-key.pem'
        SERVER_IP = '34.207.90.88'
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

        stage('SSH Test') {
            steps {
                bat """
                "%SSH%" -o StrictHostKeyChecking=no ^
                -i "%SSH_KEY%" ^
                ubuntu@%SERVER_IP% ^
                "echo CONNECTED_FROM_JENKINS"
                """
            }
        }
    }

    post {
        success {
            echo 'SSH test successful!'
        }

        failure {
            echo 'SSH test failed!'
        }
    }
}