pipeline {
  agent { label 'linux' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('thirumaleshwara-dockerhub') // Update credential ID
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t thirumaleshwara/dp-alpine:latest .' // Update Docker image name
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push thirumaleshwara/dp-alpine:latest' // Update Docker image name
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}
