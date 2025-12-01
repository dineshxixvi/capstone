pipeline {
    agent any
    stages {
        stage('Pull from GitHub') {
            steps {
                git 'https://github.com/dineshxixvi/capstone'                       
            }
        }
        stage('Deploy to AWS & Azure') {
            steps {
                sh 'cp index-aws.html /var/www/html/index-aws.html'
                sh 'cp index-azure.html /var/www/html/index-azure.html'
                sh 'sudo systemctl restart nginx'
            }
        }
    }
}
