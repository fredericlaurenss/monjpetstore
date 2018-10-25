pipeline {
  agent any
  stages {
    stage('Récupération des sources') {
      steps {
        git(url: 'https://github.com/fredericlaurenss/monjpetstore.git', branch: 'master', credentialsId: 'logingithub')
      }
    }
    stage('build Maven') {
      steps {
        bat(script: 'runmaven.bat', encoding: 'uft-8')
      }
    }
  }
}