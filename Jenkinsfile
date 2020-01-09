pipeline {
	agent any
	stages {
		stage('Source') { 
			steps {
				checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/prabhavagrawal/discoveri-happytrip.git']]])
			}
		}
		stage('Build') { 
			tools {
				jdk 'JDK8'
				maven 'Maven3'
			}
			steps {
				powershell 'java -version'
				powershell 'mvn -version'
				powershell 'mvn clean package'
				archiveArtifacts 'target/*.war'

			}
		}
		       		stage('Deploy') {
			steps{
			echo "Deploying"
			deploy adapters: [tomcat7(credentialsId: 'tomcat', path: '', url: 'http://localhost:8085/')], contextPath: 'happytrip', war: '**/*.war'
			}
		}
	}
}
