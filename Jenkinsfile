pipeline {
    agent {
        dockerfile {
            filename 'Dockerfile'
        }
    }
    environment {
        CI = 'true'
        /* Per app configured variables */
        dockerRegistry = '--some-docker-registry--'

        dockerRepo = '--some-docker-repo--'
        jenkinsJob = '--some-jenkins-job--'
        ecosystem = 'fe'
        // FORTIFY_ACCESS = credentials('48845hsdh874-hdsf7rwer87')
    }
    options {
        timestamps()
        ansiColor(colorMapName: 'xterm')
    }
    stages { 
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Unit Test') {
            steps {
                sh 'node -v'
                sh 'npm -v'
                sh 'npm run test'
            }
        }
        stage('Build DEV Docker image') {
            steps {
                lock(resource: "${jenkinsJob}", inversePrecedence: false) {
                    script {
                        gitCommit = sh(script: 'git rev-parse --short HEAD', returnStdout: true).trim()
                        version = sh(script: 'node -e "console.log(require(\'./package.json\').version)"', returnStdout: true).trim()

                        try {
                            sh "sudo docker build --rm -t ${dockerRepo}-dev ."
                            sh "sudo docker tag -f ${dockerRepo}-dev ${dockerRegistry}/${dockerRepo}-dev:${version}.${gitCommit}"
                            // sh "sudo docker push ${dockerRegistry}/${dockerRepo}-dev:${version}.${gitCommit}"
                        } catch (ex) {
                           error "Error when building DEV docker image"
                        }
                    }
                }
            }
        }
    }
}