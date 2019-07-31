pipeline {
    agent {
        // Equivalent to "docker build -f Dockerfile.build --build-arg version=1.0.2 ./build/
        dockerfile {
            filename 'Dockerfile'
            //dir 'build'
            //label 'my-defined-label'
            //additionalBuildArgs  '--build-arg version=1.0.2'
            //args '-v /tmp:/tmp'
        }
    }
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh 'node -v'
                sh 'npm -v'
                sh 'npm run test'
            }
        }
    }
}