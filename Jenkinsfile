pipeline {
  agent any
  
  environment {

    IMAGE_REPOSITORY = "sit737-23t1-arora-5acc5a5"
    SERVICE_NAME = "video-streaming"
    APP_VERSION = "${currentBuild.startTimeInMillis}"
  }
  
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t gcr.io/${env.IMAGE_REPOSITORY}/${env.SERVICE_NAME}:${APP_VERSION} .'
      }
    }
    
    stage('Test') {
      steps {
        echo "Running tests"
        npm test
      }
    }
    
    stage('Pushing image') {
      steps {
        sh 'docker push gcr.io/${env.IMAGE_REPOSITORY}/${env.SERVICE_NAME}:${APP_VERSION}'
      }
    }
  }
}