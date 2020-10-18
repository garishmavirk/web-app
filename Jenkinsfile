pipeline {
  environment {
    registry = "garishmavirk/spcm"
    registryCredential = 'garishmavirk'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/garishmavirk/web-app.git'
      }
    }
    stage('Build') {
       steps {
         sh 'docker build -t simple-web-application .'
       }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Deploy Image') {
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