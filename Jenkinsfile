pipeline {
    agent none
    environment {
        BRANCH_NAME = "${GIT_BRANCH.split("/")[1]}"
        DOCKERHUB_CREDENTIALS=credentials('dockerhub-cherkez')
        IMAGE_NAME = 'homework-image-jenkins'
        CONTAINER_NAME = 'homework-container-jenkins'
    }
    stages {
        stage('docker_lint_test') {
            agent {
                docker { 
                    image 'hadolint/hadolint:latest-alpine' }
            }
            steps {
                sh 'hadolint Dockerfile'
            }
        }
        stage('docker_build') {
            agent {
                docker { 
                    image 'docker:latest'
                    args  '-u 0' }
            }
            steps {
                sh 'docker rm --force $CONTAINER_NAME'
                sh 'docker rmi --force $DOCKERHUB_CREDENTIALS_USR/$IMAGE_NAME:$CHANGE_BRANCH'
                sh 'apk --no-cache add curl'
                sh 'docker build -t $DOCKERHUB_CREDENTIALS_USR/$IMAGE_NAME:$CHANGE_BRANCH .'
                sh 'docker run -d -p 8787:8080 --name=$CONTAINER_NAME $DOCKERHUB_CREDENTIALS_USR/$IMAGE_NAME:$CHANGE_BRANCH'
                sh 'sleep 5'
                sh 'curl --insecure http://gitlab-cherkez.pp.ua:8787 | grep "Docker HomeWork 1"'
            }
        }
    }
}