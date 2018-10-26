pipeline {
  agent any
  stages {
    stage('Recuperation des sources') {
      steps {
        git(url: 'https://github.com/fredericlaurenss/monjpetstore.git', branch: 'master', credentialsId: 'logingithub')
      }
    }
    stage('build Maven') {
      steps {
        bat(script: 'runmaven.bat', encoding: 'utf-8')
      }
    }
    stage('qualimetrie') {
      steps {
        withSonarQubeEnv('Sonar') {
          bat(script: 'runqualimetry.bat', encoding: 'utf-8')
        }

      }
    }
    stage('quality gate') {
      steps {
        sleep 10
        timeout(time: 4, unit: 'MINUTES') {
          waitForQualityGate(abortPipeline: true)
        }

      }
    }
    stage('Publication') {
      steps {
        nexusArtifactUploader(artifacts: [
                                                  				[artifactId: 'jpetstore', classifier: 'debug', file: 'target/jpetstore.war', type: 'war']
                                                  			], credentialsId: 'nexus', groupId: 'jpetstore', nexusUrl: 'localhost:8081/', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-snapshots', version: '1.0-SNAPSHOT')
        }
      }
    }
  }