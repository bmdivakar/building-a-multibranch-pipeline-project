pipeline {
  agent {
    docker {
      image "node:6-alpine"
      args "-p 5000:5000 -p 3000:3000"
    }
  }
  env {
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
  }
}
