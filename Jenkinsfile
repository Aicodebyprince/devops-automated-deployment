pipeline {
    agent any

    environment {
        SERVER_IP = '34.207.90.88'
    }

    stages {

        stage('SSH Test') {pipeline {
    agent any

    stages {

        stage('SSH Test') {
            steps {
                bat '''
                "C:\\Windows\\System32\\OpenSSH\\ssh.exe" ^
                -o StrictHostKeyChecking=no ^
                -i "C:\\JenkinsKeys\\devops-key.pem" ^
                ubuntu@34.207.90.88 ^
                "echo CONNECTED FROM JENKINS"
                '''
            }
        }

    }
}
            steps {

                sshagent(credentials: ['ec2-key']) {

                    bat '''
                    ssh -o StrictHostKeyChecking=no ubuntu@34.207.90.88 "echo CONNECTED FROM JENKINS"
                    '''

                }

            }
        }

    }
}