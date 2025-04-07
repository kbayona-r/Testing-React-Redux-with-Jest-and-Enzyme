pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'mvn clean compile'
      }
    }
    stage('Testing') {
      steps {
        sh 'mvn test'
      }
    }
  }
}
