def builderImage
def productionImage
def ACCOUNT_REGISTRY_PREFIX
def GIT_COMMIT_HASH

pipeline {
  agent any
  environment {
    GIT_COMMIT_HASH = sh "git rev-parse HEAD"
    PATH="/Users/clbrinkm/bin:/Users/clbrinkm/opt/anaconda2/condabin:/usr/local/bin:/usr/local/sbin:/usr/bin:/bin:/usr/sbin:/sbin:/opt/X11/bin"
  }
  stages {
    stage('Checkout Source Code and Logging Into Registry') {
      steps {
        echo 'Logging Into the Private Registry'
        script {
          ACCOUNT_REGISTRY_PREFIX = "codybrinkman"
        }
      }
    }

    stage('Make A Builder Image') {
      steps {
        echo 'Starting to build the project builder docker image'
        script {
          sh "whoami"
          sh "echo $PATH"
          builderImage = docker.build("codybrinkman/example-webapp-builder:${GIT_COMMIT_HASH}", "-f ./Dockerfile.builder .")
        }
      }
    }

    stage('Deploy to Production fixed server') {
      when {
        branch 'release'
      }
      steps {
        echo 'deploying release to production'
        script {
          sh "echo hi it worked"
        }
      }
    }
  }
}
