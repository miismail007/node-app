pipeline{

	agent { label 'testing-slave'}
	stages{
		stage (" Checkout code")
		{
			steps{
			checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/miismail007/node-app.git']]])	
			}
		}

	}
}
