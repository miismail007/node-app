pipeline {
     environment {
    userInput = true
  }
	agent { label 'testing-slave' }
	stages {
						  
		stage ('checkout') {
			steps {
			checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/miismail007/node-app.git']]])
			}
		}

        
        


		}
  

	}

