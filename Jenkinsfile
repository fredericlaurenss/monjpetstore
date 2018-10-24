pipeline {
  agent any
  stages {
    stage('prepare') {
      steps {
        sh 'mvn'
        sleep(unit: 'MINUTES', time: 10)
      }
    }
    stage('build') {
      steps {
        sh 'mvn'
      }
    }
  }
}