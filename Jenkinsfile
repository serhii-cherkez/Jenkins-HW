pipeline {
    stages {
        stage('test') {
            node {
                checkout scm

                docker.withServer('tcp://gitlab-cherkez.pp.ua:2376', 'swarm-certs') {
                    docker.image('hadolint/hadolint:latest-alpine').withRun('-p 3306:3306') {
                        /* do things */
        }
    }
}
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