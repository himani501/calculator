pipeline {
  environment {
    registry = "himani501/new-calculator"
    registryCredential = 'himani'
    dockerImage = ''
    dockerImageLatest = ''
  }
  agent any
    stages {

        stage('Cloning Git') {
      steps {
        git 'https://github.com/himani501/calculator.git'
      }
    }
    stage('Build Executable Jar'){
        steps {
             sh 'mvn clean test package'
        }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
          dockerImageLatest = docker.build registry + ":latest"
        }
      }
    }

    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
            dockerImageLatest.push()
          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
  }
}