pipeline {
    agent any
 
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    credentialsId: 'pat-creds',
                    url: 'https://github.com/peakyblinder0509/microservices.git'
            }
        }
 
        stage('Deploy to EC2') {
            steps {
                sshagent(['pat-creds']) {
                    sh '''
                        ssh -A -o StrictHostKeyChecking=no ubuntu@43.204.25.189 \
                            "set -e && \
                            cd /home/ubuntu/microservices && \
                            rm -rf microservices || true && \
                            git clone git@github.com:peakyblinder0509/microservices.git && \
                            cd /home/ubuntu/microservices/microservices && \
                            chmod +x clone.sh && \
                            ./clone.sh && \
                            docker-compose down || true && \
                            docker system prune -f && \
                            docker-compose up --build -d"
                    '''
                }
            }
        }
    }
}

 

















