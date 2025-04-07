pipeline {
  agent {
    docker { image 'maven:3.8.1-jdk-11' }
  }
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
