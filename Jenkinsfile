stage('Deploy To EC2') {
    steps {

        bat '''
        "C:\\Windows\\System32\\OpenSSH\\ssh.exe" ^
        -o StrictHostKeyChecking=no ^
        -i "C:\\Users\\princ\\.ssh\\devops-key.pem" ^
        ubuntu@34.207.90.88 ^
        "sudo docker stop devops-container || true &&
         sudo docker rm devops-container || true &&
         rm -rf ~/app &&
         git clone https://github.com/Aicodebyprince/devops-automated-deployment.git ~/app &&
         cd ~/app &&
         sudo docker build -t devops-website:latest . &&
         sudo docker run -d -p 80:80 --name devops-container devops-website:latest"
        '''
    }
}