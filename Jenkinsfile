pipeline {
    agent any

    stages {

        stage('Deploy To EC2') {

            steps {

                bat '''
                "C:\\Windows\\System32\\OpenSSH\\ssh.exe" ^
                -o StrictHostKeyChecking=no ^
                -i "C:\\Users\\princ\\.ssh\\devops-key.pem" ^
                ubuntu@34.207.90.88 ^
                "echo CONNECTED"
                '''

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