pipeline {
  agent {
    docker { image 'hadolint/hadolint:latest-alpine' }
  }
  stages {
    stage('Test') {
      steps {
        sh 'hadolint Dockerfile'
      }
    }
  }
}