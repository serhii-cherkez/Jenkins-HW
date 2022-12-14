pipeline {
    agent docker
    environment {
        DOCKERHUB_CREDENTIALS=credentials('dockerhub-cherkez')
        IMAGE_NAME = 'homework-image-jenkins'
        CONTAINER_NAME = 'homework-container-jenkins'
    }
    stages {
        stage('docker_lint_test') {
            image 'hadolint/hadolint:latest-alpine'
                steps {
                    sh 'hadolint Dockerfile'
            }
        }
        stage('docker_build') {
            image 'docker:latest'
            args  '-u 0' 
                steps {
                    sh 'docker rm --force $CONTAINER_NAME'
                    sh 'docker rmi --force $DOCKERHUB_CREDENTIALS_USR/$IMAGE_NAME:$BRANCH_NAME'
                    sh 'apk --no-cache add curl'
                    sh 'docker build -t $DOCKERHUB_CREDENTIALS_USR/$IMAGE_NAME:$BRANCH_NAME .'
                    sh 'docker run -d -p 8585:8080 --name=$CONTAINER_NAME $DOCKERHUB_CREDENTIALS_USR/$IMAGE_NAME:$BRANCH_NAME'
                    sh 'sleep 5'
                    sh 'curl --insecure http://gitlab-cherkez.pp.ua:8585 | grep "Docker HomeWork 1"'
            }
        }
        stage('docker_push') {
            when {
                changeRequest target: '$BRANCH_MAIN'
            }
            image 'docker:latest'
            args  '-u 0' 
                steps {
                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                    sh 'docker push $DOCKERHUB_CREDENTIALS_USR/$IMAGE_NAME:$BRANCH_NAME'
                
            }
        }
    }
}