pipeline {
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/Egwonor/book-api.git'
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build ovoh1/bookinventory + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', dockerhub ) {
            dockerImage.push()
          }
        }
      }
    }
   } 
 }  