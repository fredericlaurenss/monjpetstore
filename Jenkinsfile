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
	stage('Publication'){
		steps {
			nexusArtifactUploader(nexusVersion : 'nexus3', protocol : 'http',  nexusUrl : 'localhost:8081/', groupId : 'jpetstore', version : '1.0', repository : 'maven-snapshots', credentialsId : 'nexus', artifact : {
				artifactId : 'jpetstore', type : 'war', classifier : 'debug', file : 'target/jpetstore.war'}
		  }
		}
		}
  }
}