pipeline {
  environment {
    registry = "rsansh/cyberfrat-devsecops"
    registryCredential = "DockerHub"
    dockerImage = ''
  }
  agent any
 
  stages {
    stage('Build Docker Image') {
      steps {
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER" 
        }
      }
    }
    
    stage('Push to DockerHub') {
      steps {
        script {
          docker.withRegistry('',registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    
    stage('Test Run') {
      steps {
        sh 'docker run -d $registry:$BUILD_NUMBER'
      }
    }
  }
}
