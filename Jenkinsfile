pipeline {
  agent any
  parameters {
    choice(name: 'VERSION', choices: ['1.1.0', '1.2.3', '1.2.1'], description:'default values')
    booleanParam(name: 'executeTests', defaultValue: true, description: '')
    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
    password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')

    text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
  }
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
          bat 'mvn --version'
          echo  "my name is ${params.PERSON}"
          echo  "my name is ${params.BIOGRAPHY}"
          echo  "my name is ${params.PASSWORD}"
          echo  "my name is ${params.VERSION}"
          echo  "my name is ${params.executeTests}"
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
