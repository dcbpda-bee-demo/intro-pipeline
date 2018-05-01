pipeline {
  agent {
    label 'jdk9'
  }
  stages {
    stage('Hello') {
      steps {
        echo 'Hello World'
        sh '''java -version 
'''
      }
    }
  }
}