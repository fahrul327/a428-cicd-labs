node {
    def dockerImage = 'node:lts-buster-slim'

    stage('Build') {
        agent {
            docker {
                image dockerImage
                args '-p 3000:3000'
            }
        }
        environment {
            CI = 'true'
        }
        steps {
            sh 'npm install'
        }
    }

    stage('Test') {
        agent {
            docker {
                image dockerImage
            }
        }
        steps {
            sh './jenkins/scripts/test.sh'
        }
    }

    stage('Deliver') {
        agent {
            docker {
                image dockerImage
            }
        }
        steps {
            sh './jenkins/scripts/deliver.sh'
            input message: 'Finished using the web site? (Click "Proceed" to continue)'
            sh './jenkins/scripts/kill.sh'
        }
    }
}
