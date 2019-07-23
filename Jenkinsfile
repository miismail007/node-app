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
		
	 stage (" ENV: TEST - Run the Container")
	{
	   steps{
		   sh "docker run -d -p 8080:80 helloarcbuild:v1"	
	  	}
	 }
		
	stage("ENV: Production - Run the Container for Approval")
		{
			agent { label 'production-slave'}
			options {
				timeout(time: 30, unit: 'MINUTES')
			}
			input {
				message : "MR.Shiva can you please Approve or Decined Production Deployment!"
				ok "Deploy"
				parameters {
					choice(name: 'Choice', choice: "Yes\nNo",description: "Please confirm to deploy?")
					
				}
			}
			
			steps {
				checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/miismail007/node-app.git']]])	
				echo "Option selected as ${Choice}"
			}
		}
		
		
		
		
		

	}
}
