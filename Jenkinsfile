pipeline {
  agent any
  tools {
    nodejs 'node-uts'  // harus sama dengan nama yang kamu kasih di konfigurasi
  }
  stages {
    stage('Check Node & npm') {
      steps {
        sh 'node -v'
        sh 'npm -v'
      }
    }
    stage('Install Dependencies') {
      steps {
        sh 'npm ci'
      }
    }
    stage('Run Tests') {
      steps {
        sh 'npm test'
      }
    }
  }
}
