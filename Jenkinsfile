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

        stage ('Build') {
			steps {
			sh "docker build -t helloacrbuild:v1 ."
			}
		}
		
		stage ('Testing : Run Docker Cotainer') {
			steps {
			sh "docker run -d -p 8080:80 helloacrbuild:v1"
			}
		}
        


		}
  

	}

