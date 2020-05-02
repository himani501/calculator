pipeline {
  environment {
    registry = "himani501/new-calculator"
    registryCredential = 'himani'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
     checkout scm
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Push Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }

  }
}