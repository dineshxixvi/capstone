pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/dineshxixvi/capstone.git',
                branch: 'main'
            }
        }

        stage('Deploy to Nginx') {
            sshagent(credentials: ['06d61196-7529-44e3-a393-d8ff1ee6d5d3']) {
                steps {
                    sh '''
                        echo "Copying files to Nginx web root"
                        scp index-aws.html ubuntu@3.235.196.243:/var/www/html/
                    '''
                      }
                  }
            sshagent(credentials: ['491f17e4-55c2-4443-ad3e-4263144ac78f']) {
                steps {
                    sh '''
                        echo "Copying files to Nginx web root"
                        scp index-azure.html azureuser@20.83.178.169:/var/www/html/
                    '''
                }
            }
        }

        stage('Restart Nginx') {
            sshagent(credentials: ['06d61196-7529-44e3-a393-d8ff1ee6d5d3']) {
                steps {
                    sh '''
                        echo "Restarting Nginx service"
                        ssh ubuntu@3.235.196.243 "sudo systemctl reload nginx"
                    '''
                      }
                  }
            sshagent(credentials: ['491f17e4-55c2-4443-ad3e-4263144ac78f']) {
                steps {
                    sh '''
                        echo "Restarting Nginx service"
                        ssh azureuser@20.83.178.169 "sudo systemctl reload nginx"
                    '''
                      }
                }
            }
        }
    }
