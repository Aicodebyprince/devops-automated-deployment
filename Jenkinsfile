pipeline {
    agent any

    stages {

        stage('Test SSH Connection') {
            steps {

                sshagent(credentials: ['ec2-key']) {

                    bat '''
                    ssh -o StrictHostKeyChecking=no ubuntu@34.207.90.88 "echo Connected Successfully"
                    '''

                }

            }
        }

    }
}