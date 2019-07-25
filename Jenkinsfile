pipeline {
    agent { docker { image '10.16.0-alpine' } }
    stages {
        stage('build') {
            steps {
                sh 'npm --version'
            }
        }
    }
}
