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
          GIT_COMMIT_HASH = sh (script: "git log -n 1 --pretty=format: '%H'", returnStdout: true)
          ACCOUNT_REGISTRY_PREFIX = "https://hub.docker.com/repository/docker/codybrinkman/example-webapp"
        }
      }
    }
  }
}
