pipeline {
  agent { label 'seed-job-agent' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('thirumaleshwara-dockerhub') // Update credential ID
  }
  stages {
    stage('Build') {
      steps {
        script {
          node {
            sh 'docker build -t thirumaleshwara/dp-alpine:latest .' // Update Docker image name
          }
        }
      }
    }
    stage('Login') {
      steps {
        script {
          node {
            sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
          }
        }
      }
    }
    stage('Push') {
      steps {
        script {
          node {
            sh 'docker push thirumaleshwara/dp-alpine:latest' // Update Docker image name
          }
        }
      }
    }
  }
  post {
    always {
      script {
        node {
          sh 'docker logout'
        }
      }
    }
  }
}
