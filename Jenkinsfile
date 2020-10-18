pipeline {
  agent any
  tools {
        maven 'Maven'
  }
  triggers { pollSCM('H/2 * * * *') }
  environment {
    ACCESS_KEY = credentials('git-pass')
  }
  stages {
    stage('build') {
      when {
        expression {
          BRANCH_NAME == 'Dev'
        }
      }
      steps {
        echo 'we are in Dev build stage'
      }
    }
    stage('test') {
      when {
        expression {
          BRANCH_NAME == 'main'
        }
      }
      steps {
          echo 'test stage in main branch with pollSCM'
      }
    }
    stage('deploy') {
      steps {
          echo 'deploy stage'
          echo "The Jenkins URL is ${JENKINS_URL}"
          echo "The user name is  ${ACCESS_KEY_USR}"
          bat "mvn --version"
      }
    }
  }
    post {
        always {
      echo 'One way or another, I have finished'
        //deleteDir() /* clean up our workspace */
        }
        success {
      echo 'I succeeded!'
        }
        unstable {
      echo 'I am unstable :/'
        }
        failure {
      echo 'I failed :('
        }
        changed {
      echo 'Things were different before...'
        }
    }
}
