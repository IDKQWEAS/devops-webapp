pipeline {
    agent any

    tools {
        nodejs "Node18"  // Sesuaikan dengan nama NodeJS tool di Jenkins
    }

    environment {
        DEPLOY_USER = "ec2-user"
        DEPLOY_HOST = "3.0.19.184"  // Ganti dengan IP publik server Anda
        SSH_CREDENTIALS_ID = "zidan_ssh"  // ID credential SSH di Jenkins
        APP_DIR = "/home/ec2-user/app/uts-devopss"
        GIT_REPO = "https://github.com/IDKQWEAS/devops-webapp.git"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'development', url: "${GIT_REPO}"
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test || echo "No tests defined"'
            }
        }

        stage('Build') {
            steps {
                sh 'node -v'
                sh 'npm install'
                // sh 'npm run build'
            }
        }
        stage('Deploy') {
          steps {
            sshagent(['your-credentials-id']) {
              sh 'scp -o StrictHostKeyChecking=no -i ~/.ssh/zidan ...'
            }
          }
        }

        stage('Deploy') {
            when {
                expression { currentBuild.currentResult == 'SUCCESS' }
            }
            steps {
                sshagent([SSH_CREDENTIALS_ID]) {
                    sh """
                    ssh -o StrictHostKeyChecking=no ${DEPLOY_USER}@${DEPLOY_HOST} << 'ENDSSH'
                    if [ ! -d "${APP_DIR}" ]; then
                        mkdir -p /home/ec2-user/app
                        cd /home/ec2-user/app
                        git clone ${GIT_REPO}
                    fi

                    cd ${APP_DIR}
                    git pull origin development
                    npm install

                    if ! command -v pm2 &> /dev/null; then
                        sudo npm install -g pm2
                    fi

                    pm2 restart app.js || pm2 start app.js
ENDSSH
                    """
                }
            }
        }
    }

    post {
        success {
            echo "Pipeline finished successfully."
        }
        failure {
            echo "Pipeline failed. Check the logs."
        }
    }
}
