pipeline {
    agent any

    tools {
        nodejs 'Node18'  // Harus sama seperti yang dikonfigurasi di Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }
    }

    post {
        success {
            echo '✅ Build sukses'
        }
        failure {
            echo '❌ Build gagal'
        }
    }
}
