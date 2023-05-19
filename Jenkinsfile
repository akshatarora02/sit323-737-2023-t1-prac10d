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
        dir('video-streaming/') {
          sh "docker build -t gcr.io/${env.IMAGE_REPOSITORY}/${env.SERVICE_NAME}:${env.APP_VERSION} ."
        }
      }
    } 
    stage('Test') {
      steps {
        echo "Running tests"
        sh "docker run --rm gcr.io/${env.IMAGE_REPOSITORY}/${env.SERVICE_NAME}:${env.APP_VERSION} npm test"

      }
    }
      stage('Pushing image') {
      steps {
        sh "docker push gcr.io/${env.IMAGE_REPOSITORY}/${env.SERVICE_NAME}:${env.APP_VERSION}"
      }
    }
  }
  stage('Write Value to File') {
            steps {
                script {
                    def filePath = 'var/lib/jenkins/dockerversion.txt'
                    def file = new File(filePath)
                    def value = ${env.APP_VERSION}
                    if (!file.exists()) {
                        file.createNewFile()
                    }
                    file.write(value)
                    file.close()
                }
            }
        }

}