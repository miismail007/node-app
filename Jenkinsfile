pipeline{

	agent { label 'testing-slave'}
	stages{
		stage (" Checkout code")
		{
			steps{
			checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/miismail007/node-app.git']]])	
			}
		}
			
		stage ("Build Docker Cotainer Image") {
		steps {		
		
			sh "docker build -t helloarcbuild:v1 ."
		}
		}
		
	stage (" Run the Container")
		{
			steps{
			sh "docker run -d -p 8080:80 helloarcbuild:v1"	
			}
		}
		

	}
}
