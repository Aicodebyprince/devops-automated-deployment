pipeline {
    agent any

    environment {
        DOCKER = 'C:\\Users\\princ\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe'
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

        stage('Deploy To EC2') {
            steps {

                sshagent(credentials: ['ec2-key']) {

                    bat """
                    ssh -o StrictHostKeyChecking=no ubuntu@%SERVER_IP% ^
                    "sudo docker stop devops-container || true && ^
                    sudo docker rm devops-container || true && ^
                    rm -rf ~/app && ^
                    git clone https://github.com/Aicodebyprince/devops-automated-deployment.git ~/app && ^
                    cd ~/app && ^
                    sudo docker build -t devops-website:latest . && ^
                    sudo docker run -d -p 80:80 --name devops-container devops-website:latest"
                    """

                }
            }
        }

        stage('Verify Deployment') {
            steps {

                sshagent(credentials: ['ec2-key']) {

                    bat """
                    ssh -o StrictHostKeyChecking=no ubuntu@%SERVER_IP% ^
                    "sudo docker ps"
                    """

                }
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