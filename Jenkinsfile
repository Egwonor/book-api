pipeline {
    agent any

    triggers {
        pollSCM '* * * * *'
    }
    stages {
        stage('Clone repo') {
            steps {
             git 'https://github.com/Egwonor/book-api.git'
            }
        }
        stage('Build image') {
            steps {
             sh  'docker build -t bookinventory .'   
            }
        }
    }
}