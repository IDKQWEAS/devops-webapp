pipeline {
  agent any

  environment {
    NODE_ENV = 'development'
  }

  stages {
    stage('Checkout Code') {
      steps {
        checkout scm
      }
    }

    stage('Install Dependencies') {
      steps {
        echo 'Installing dependencies...'
        sh 'npm ci' // lebih cepat & konsisten daripada 'npm install'
      }
    }

    stage('Run Tests') {
      steps {
        echo 'Running test suite...'
        sh 'npm test'
      }
    }
  }

  post {
    success {
      echo '✅ Build and test succeeded!'
    }
    failure {
      echo '❌ Build or test failed!'
    }
  }
}
