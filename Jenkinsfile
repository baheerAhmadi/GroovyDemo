pipeline {
  agent any
  triggers { pollSCM('H/2 * * * *') }
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
      steps {
          echo 'test stage with pollSCM'
      }
    }
    stage('deploy') {
      steps {
          echo 'deploy stage'
          echo "The Jenkins URL is ${JENKINS_URL}"
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
