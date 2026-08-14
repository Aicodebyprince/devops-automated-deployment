pipeline {
    agent any

    environment {
        SERVER_IP = '34.207.90.88'
    }

    stages {

        stage('SSH Test') {
            steps {

                sshagent(['ec2-key']) {

                    bat '''
                    ssh -o StrictHostKeyChecking=no ubuntu@34.207.90.88 "echo CONNECTED FROM JENKINS"
                    '''

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