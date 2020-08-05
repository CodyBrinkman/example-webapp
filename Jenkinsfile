def builderImage
def productionImage
def ACCOUNT_REGISTRY_PREFIX
def GIT_COMMIT_HASH

pipeline {
  agent any
  environment {
    PATH="/Users/clbrinkm/bin:/Users/clbrinkm/opt/anaconda2/condabin:/usr/local/bin:/usr/local/sbin:/usr/bin:/bin:/usr/sbin:/sbin:/opt/X11/bin"
  }
  stages {
    stage('Checkout Source Code and Logging Into Registry') {
      steps {
        echo 'Logging Into the Private Registry'
        script {
          GIT_COMMIT_HASH = sh (
            script: "git rev-parse HEAD",
            returnStdout: true)
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
          builderImage = docker.build("codybrinkman/example-webapp-builder:123", "-f ./Dockerfile.builder .")
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

    stage('Integration Tests') {
      steps {
        echo 'Testing...'
        script {
          sh """
            curl -v localhost:3000 | grep '<title>Welcome to example-webapp</title>'
            if [ \$? -eq 0 ]
            then
              echo test pass
            else
              echo test failed
              exit 1
            fi
          """
        }
      }
    }
  }
}
