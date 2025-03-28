pipeline {
  agent any
  stages {
    stage('Clone repository') {
      steps {
        checkout scm
      }
    }

    stage('Build image') {
      steps {
        script {
          app = docker.build("${IMAGE_NAME}")
        }

      }
    }

    stage('Push image') {
      steps {
        script {
          docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDENTIALS_ID) {
            def branch = env.BRANCH_NAME ?: 'main'
            app.push("${branch}-${env.BUILD_NUMBER}")
            app.push("${branch}-latest")
          }
        }

      }
    }

    stage('End ') {
      steps {
        echo 'Done'
      }
    }

  }
  environment {
    DOCKER_CREDENTIALS_ID = 'docker-hub'
    IMAGE_NAME = 'dariyozz/jenkins-blueocean'
  }
}