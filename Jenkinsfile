pipeline {
  agent any
  environment {
  # ubah 'youruser/simple-app' dengan nama kamu dan repo proyek kamu
    IMAGE_NAME = 'wahyuditrs17/simple-app'
    REGISTRY = 'https://index.docker.io/v1/'
  # ubah 'dockerhub-credentials' dengan credential yang sudah kamu buat 
    REGISTRY_CREDENTIALS = 'dckr_pat_RF3gXBJCJc5h06_DvkkuMw_uaYk'
  }
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Build') {
      steps {
        sh 'echo "Mulai build aplikasi"'
      }
    }
    stage('Build Docker Image') {
      steps {
        script {
          docker.build("${env.IMAGE_NAME}:${env.BUILD_NUMBER}")
        }
      }
    }
    stage('Push Docker Image') {
      steps {
        script {
          docker.withRegistry(env.REGISTRY, env.REGISTRY_CREDENTIALS) {
            def tag = "${env.IMAGE_NAME}:${env.BUILD_NUMBER}"
            docker.image(tag).push()
            docker.image(tag).tag('latest')
            docker.image("${env.IMAGE_NAME}:latest").push()
          }
        }
      }
    }
  }
  post {
    always {
      echo 'Selesai build'
    }
  }
}
