pipeline {
    agent none
    stages {
        stage('Test') {
            agent {
                docker { image 'hadolint/hadolint:latest-alpine' }
            }
            steps {
                sh 'hadolint Dockerfile'
            }
        }
    }
}  