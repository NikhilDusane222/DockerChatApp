pipeline {
	agent any
	stages {
		stage('Sonarqube') {
			enviornment {
				scannerHome  = tool 'sonarScanner'
			}
			steps {
				withSonarQubeEnv('sonarqube') {
					sh "${scannerHome}/bin/sonarScanner"
				}
				timeout(time: 5, unit: 'MINUTES') {
					waitForQualityGate abortPipeline: true
				}
			}    
		}  
		stage('Deploy') { 
			steps {
				sh ''' #! /bin/bash 
				aws deploy create-deployment --application-name jenkinApp --deployment-group-name jenkindeploy --deployment-config-name CodeDeployDefault.AllAtOnce --github-location repository=tushar8871/chatApplication,commitId=${GIT_COMMIT}
				'''
			}
		}
	}
	post {
		always {
			echo "Stages are executed successfully"   
		}
	}
}
