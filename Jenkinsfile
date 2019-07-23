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
		
		stage ('Run Docker Cotainer') {
			steps {
			sh "docker run -d -p 8080:80 helloacrbuild:v1"
			}
		}

 stage('Deploy') {
 agent {  label 'production-slave' }
	
      options {
        timeout(time: 30, unit: 'MINUTES') 
      }
      input {
        message "Which Version?"
        ok "Deploy"
        parameters {
            choice(name: 'APP_VERSION', choices: "yes\nno", description: 'What to deploy?')
        }
      }
      steps {
	  checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/miismail007/node-app.git']]])
        echo "Deploying ${APP_VERSION}."
      }
    }


		}
  

	}

