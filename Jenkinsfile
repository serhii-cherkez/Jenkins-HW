pipeline {
    agent docker
    
    stages {
        stage 'test' {
            agent {
                label 'docker-jnlp-agent' {
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