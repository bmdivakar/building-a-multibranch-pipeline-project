pipeline {
  agent {
    docker {
      image "node:current-alpine"
      args "-p 5000:5000 -p 3000:3000"
    }
  }
  environment {
    CI = "true"
  }
  stages {
    stage('Build'){
      steps {
        sh 'npm install'
      }
    }
    stage('Test'){
      steps{
        sh './jenkins/scripts/test.sh'
      }
    }
    stage('Deliver for Development'){
      when {
        branch 'development'
      }
      steps{
        sh './jenkins/scripts/deliver-for-development.sh'
        input message:'Completed using the webpage? (Click "Proceed" to continue)'
        sh './jenkins/scripts/kill.sh'
      }
    }
    stage('Deliver for Production') {
      when {
        branch 'production'
      }
      steps {
        sh './jenkins/scripts/deliver-for-production.sh'
        input message:'Completed using the webpage? (Click "Proceed" to continue)'
        sh './jenkins/scripts/kill.sh'
      }
    } 
  }
}
