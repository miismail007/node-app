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
        message "can you please Approve or Decline production deployment?"
        ok "Deploy"
        parameters {
            choice(name: 'Choice Yes or No', choices: "Yes\nNo", description: 'Continure the production deployment?')
        }
      }
      steps {
	  checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/miismail007/node-app.git']]])
     sh "docker build -t helloacrbuild:v1 ."
	      sh "docker run -d -p 8080:80 helloacrbuild:v1"
      }

    }


		}
  

	}

