pipeline {
    agent { docker { image 'node:10' } }
    stages {
        stage('build') {
            steps {
                sh 'npm -v'
                sh 'node -v'
            }
        }
    }
}
