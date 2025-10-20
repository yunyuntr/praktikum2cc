pipeline { 
  agent any 
  environment { 
    IMAGE_NAME = 'wahyuditrs17/simple-app' 
    REGISTRY_CREDENTIALS = 'dockerhub-credentials' 
  } 
  stages { 
    stage('Checkout') { steps { checkout scm } } 
    stage('Build') { steps { bat 'echo "Build di Windows"' } } 
    stage('Build Docker Image') { steps { bat "docker build -t %IMAGE_NAME%:%BUILD_NUMBER% ." } } 
    stage('Push Docker Image') { 
      steps { 
        withCredentials([usernamePassword(credentialsId: REGISTRY_CREDENTIALS, usernameVariable: 'USER', passwordVariable: 'PASS')]) { 
          bat 'docker login -u %USER% -p %PASS%' 
          bat "docker push %IMAGE_NAME%:%BUILD_NUMBER%" 
          bat "docker tag %IMAGE_NAME%:%BUILD_NUMBER% %IMAGE_NAME%:latest" 
          bat "docker push %IMAGE_NAME%:latest" 
        } 
      }
}
}
}
