def builderImage
def productionImage
def ACCOUNT_REGISTRY_PREFIX
def GIT_COMMIT_HASH

pipeline {
  agent any
  stages {
    stage('Checkout Source Code and Logging Into Registry') {
      steps {
        echo 'Logging Into the Private Registry'
        script {
          GIT_COMMIT_HASH = sh "git rev-parse HEAD"
          ACCOUNT_REGISTRY_PREFIX = "codybrinkman"
        }
      }
    }

    stage('Make A Builder Image') {
      steps {
        echo 'Starting to build the project builder docker image'
        script {
          sh "echo hi"
          builderImage = docker.build("${ACCOUNT_REGISTRY_PREFIX}/example-webapp-builder:51cf4f8d5415dd5bc849269ead75021e0feb81f8", "-f ./Dockerfile.builder .")
        }
      }
    }
  }
}
