pipeline {
  environment {
    registryName = "ovoh1"
    registry = "ovoh1/book-inventory"
    registryCredential = 'dockerhub'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/lovely-007/book-api.git'
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
    stage('Deploy to AWS') {
            steps {
                withAWS(credentials: 'aws-credentials', region: env.REGION) {
                    bat './gradlew awsCfnMigrateStack -PsubnetId=$SUBNET_ID -PdockerHubUsername=registryName -Pregion=$REGION'
                }
             }
        }
  }
}