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

        stage('Verify Image') {
            steps {
                bat "\"%DOCKER%\" images"
            }
        }

        stage('Deploy to EC2 via Ansible') {
            steps {
                bat '''
                wsl bash -c "
                cd /mnt/c/Users/princ/OneDrive/Desktop/Deveops_assignment &&
                ansible-playbook -i ansible/inventory.ini ansible/deploy.yml --private-key ~/.ssh/devops-key.pem
                "
                '''
            }
        }
    }

    post {
        success {
            echo 'GitHub → Jenkins → Ansible → EC2 Deployment Successful!'
        }

        failure {
            echo 'Deployment Failed!'
        }
    }
}