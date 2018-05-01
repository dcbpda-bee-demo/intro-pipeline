pipeline {
  agent {
    label 'jdk8'
  }
  stages {
    stage('Hello') {
      steps {
        echo "Hello ${MY_NAME}!"
        echo "${TEST_USER_USR}"
        echo "${TEST_USER_PSW}"
        echo "Hello ${params.Name}!"
        sh 'java -version '
      }
    }
    stage('Checkpoint') {
         agent none
         steps {
            checkpoint 'Checkpoint'
         }
      }
      stage('Testing') {
        failFast true
        parallel {
          stage('Java 8') {
            agent { label 'jdk9' }
            steps {
              sh 'java -version'
              sleep time: 2, unit: 'SECONDS'
            }
          }
          stage('Java 9') {
            agent { label 'jdk9' }
            steps {
              sh 'java -version'
              sleep time: 4, unit: 'SECONDS'
            }
          }
        }
      }    
    stage('Get Kernel') {
      steps {
        script {
          try {
            KERNEL_VERSION = sh (script: "uname -r", returnStdout: true)
          } catch(err) {
            echo "CAUGHT ERROR: ${err}"
            throw err
          }
        }
      }
    }
    stage('Say Kernel') {
      steps {
        echo "${KERNEL_VERSION}"
      }
    }    
  }
  environment {
    MY_NAME = 'Mary'
    TEST_USER = credentials('test-user')
  }
  parameters {
    string(name: 'Name', defaultValue: 'whoever you are', description: 'Who should I say hi to?')
  }
  post {
    aborted {
      echo 'Why didn\'t you push my button?'
    }
  }  
}
