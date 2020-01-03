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
				jdk 'jdk8'
				maven 'apache-maven-3.6.1'
			}
			steps {
				powershell 'java -version'
				powershell 'mvn -version'
				powershell 'mvn clean package'

			}
		}
		stage('Deploy') {
			steps{
				echo "Deploying"
				deploy adapters: [tomcat7(credentialsId: '98e9cbd9-106c-4efa-8238-9888f9bc8fc3', path: '', url: 'http://localhost:8082')], contextPath: 'happytrip', war: '**/*.war'
			}
		}
		
		stage('Email Notification')
		{
			steps{
				
				mail bcc: '', body: '''Hi,

                              Welcome to Jenkins email alert..This is from Happytrip build

                             Thanks ,
                              Chithra Nair''', cc: '', from: '', replyTo: '', subject: 'Jenkins Alert', to: 'testautomation865@gmail.com'		
			
			}
			
		}	
	}
}
