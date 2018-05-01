pipeline {
  agent {
    label 'jdk8'
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