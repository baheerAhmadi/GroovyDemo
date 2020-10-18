pipeline {
  agent any
  environment {
    NEW_VERSION = '1.2.3'
  }
  stages {
    stage('build') {
      steps {
        echo "build stage ${NEW_VERSION}"
      }
    }
    stage('test') {
      steps {
          echo 'test stage'
      }
    }
    stage('deploy') {
      steps {
          echo 'deploy stage'
      }
    }
  }
}
