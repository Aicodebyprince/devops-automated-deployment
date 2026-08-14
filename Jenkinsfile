pipeline {
    agent any

    environment {
        DOCKER = 'C:\\Users\\princ\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe'
        SSH = 'C:\\Windows\\System32\\OpenSSH\\ssh.exe'
        SERVER_IP = '34.207.90.88'
        SSH_KEY = 'C:\\Users\\princ\\.ssh\\devops-key.pem'
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

        stage('Test SSH Connection') {
            steps {
                bat """
                "%SSH%" -o StrictHostKeyChecking=no -i "%SSH_KEY%" ubuntu@%SERVER_IP% "echo Connected to EC2"
                """
            }
        }

        stage('Deploy To EC2') {
            steps {
                bat """
                "%SSH%" -o StrictHostKeyChecking=no -i "%SSH_KEY%" ubuntu@%SERVER_IP% "sudo docker stop devops-container; sudo docker rm devops-container; rm -rf ~/app; git clone https://github.com/Aicodebyprince/devops-automated-deployment.git ~/app; cd ~/app; sudo docker build -t devops-website:latest .; sudo docker run -d -p 80:80 --name devops-container devops-website:latest"
                """
            }
        }

        stage('Verify Deployment') {
            steps {
                bat """
                "%SSH%" -o StrictHostKeyChecking=no -i "%SSH_KEY%" ubuntu@%SERVER_IP% "sudo docker ps"
                """
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