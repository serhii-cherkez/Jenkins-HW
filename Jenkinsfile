pipeline {
    agent {docker-jnlp-agent}
    stages {
        stage('test') {
            agent {
                docker {
                    image 'hadolint/hadolint:latest-alpine'
                    reuseNode true
                }
            }
            steps {
                hadolint Dockerfile
            }
        }
    }
}