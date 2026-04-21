pipeline {
    agent any
 
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    credentialsId: 'git-cred- peaky',
                    url: 'https://github.com/peakyblinder0509/microservices.git'
            }
        }
 
        stage('Deploy to EC2') {
            steps {
                sshagent(['crm-creds']) {
                    sh '''
                        ssh -A -o StrictHostKeyChecking=no ubuntu@13.201.117.1 \
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

 

















