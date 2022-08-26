pipeline {
    agent none
    environment {
        DOCKERHUB_CREDENTIALS=credentials('dockerhub-cherkez')
        IMAGE_NAME = 'homework-image-jenkins'
        CONTAINER_NAME = 'homework-container-jenkins'
    }
    stages {
        stage('docker_lint_test') {
            agent {
                docker { image 'hadolint/hadolint:latest-alpine' }
            }
            steps {
                sh 'hadolint Dockerfile'
            }
        stage('docker_build') {
            agent {
                docker { image 'docker:latest' }
            }
            steps {
                sh 'docker rm --force $CONTAINER_NAME'
                sh 'docker rmi --force $DOCKERHUB_CREDENTIALS_USR/$IMAGE_NAME:$BRANCH_NAME'
                sh 'apk --no-cache add curl'
                sh 'docker build -t $DOCKERHUB_CREDENTIALS_USR/$IMAGE_NAME:$BRANCH_NAME .'
                sh 'docker run -d -p 8888:8080 --name=$CONTAINER_NAME $DOCKERHUB_CREDENTIALS_USR/$IMAGE_NAME:$BRANCH_NAME'
                sh 'sleep 5'
                sh 'curl --insecure http://gitlab-cherkez.pp.ua:8787 | grep "Docker HomeWork 1"'
            }
        }
    }
}
}