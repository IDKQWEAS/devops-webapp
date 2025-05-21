pipeline {
    agent any
    stages {
        stage('Check Node and npm') {
            steps {
                sh 'node -v || echo "Node not found"'
                sh 'npm -v || echo "npm not found"'
                sh 'echo $PATH'
                sh 'which node || echo "node not found in PATH"'
                sh 'which npm || echo "npm not found in PATH"'
            }
        }
        // stage lain ...
    }
}
