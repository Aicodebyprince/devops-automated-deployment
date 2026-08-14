pipeline {
    agent any

    environment {
        DOCKER = 'C:\\Users\\princ\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe'
        SSH = 'C:\\Windows\\System32\\OpenSSH\\ssh.exe'
        SSH_KEY = 'C:\\JenkinsKeys\\devops-key.pem'
        SERVER_IP = '34.207.90.88'
        REPOSITORY = 'https://github.com/Aicodebyprince/devops-automated-deployment.git'
    }

    stages {

        stage('Checkout Source') {
            steps {
                checkout scm
            }
        }

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

        stage('Test EC2 SSH') {
            steps {
                bat "\"%SSH%\" -o StrictHostKeyChecking=no -i \"%SSH_KEY%\" ubuntu@%SERVER_IP% \"echo CONNECTED_FROM_JENKINS\""
            }
        }

        stage('Deploy To EC2') {
            steps {
                bat "\"%SSH%\" -o StrictHostKeyChecking=no -i \"%SSH_KEY%\" ubuntu@%SERVER_IP% \"sudo docker rm -f devops-container 2>/dev/null; rm -rf ~/app; git clone %REPOSITORY% ~/app; cd ~/app; sudo docker build -t devops-website:latest .; sudo docker run -d -p 80:80 --name devops-container devops-website:latest\""
            }
        }

        stage('Verify Deployment') {
            steps {
                bat "\"%SSH%\" -o StrictHostKeyChecking=no -i \"%SSH_KEY%\" ubuntu@%SERVER_IP% \"sudo docker ps --filter name=devops-container\""
            }
        }

        stage('Verify Website') {
            steps {
                bat "\"%SSH%\" -o StrictHostKeyChecking=no -i \"%SSH_KEY%\" ubuntu@%SERVER_IP% \"curl -I http://localhost\""
            }
        }
    }

    post {
        success {
            echo '=============================================='
            echo 'DEPLOYMENT SUCCESSFUL'
            echo 'GitHub -> Jenkins -> Docker -> AWS EC2'
            echo '=============================================='
            echo 'Website: http://34.207.90.88'
        }

        failure {
            echo '=============================================='
            echo 'DEPLOYMENT FAILED'
            echo 'Check the failed stage in Console Output'
            echo '=============================================='
        }

        always {
            echo 'Pipeline execution completed.'
        }
    }
}