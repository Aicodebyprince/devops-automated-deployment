pipeline {
    agent any

    environment {
        SERVER_IP = '34.207.90.88'
    }

    stages {

        stage('Test SSH Connection') {
            steps {

                sshagent(credentials: ['ec2-key']) {

                    bat """
                    ssh -o StrictHostKeyChecking=no ubuntu@%SERVER_IP% "echo SUCCESS"
                    """

                }

            }
        }

    }

    post {

        success {
            echo 'SSH Connection Successful!'
        }

        failure {
            echo 'SSH Connection Failed!'
        }

    }
}