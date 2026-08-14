pipeline {
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