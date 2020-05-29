pipeline {
	agent any
	stages {
		stage('Clone Repository') {
			steps {
				sh ''' #! /bin/bash
				ssh -i /var/lib/jenkins/.ssh/id_rsa root@13.234.238.25 '
				rm -rf /chatApplication/
				'
				scp -r /var/lib/jenkins/workspace/chatApplication root@13.234.238.25:
				'''
			}
		}
		stage('Build Image') {
			steps {
				sh ''' #! /bin/bash
				ssh -i /var/lib/jenkins/.ssh/id_rsa root@13.234.238.25 '
				cd chatApplication/
				 $(aws ecr get-login --registry-ids 296838539158 --no-include-email --region  ap-south-1)
				docker-compose down 
				docker-compose up -d
				'
				'''
			}
		}
 
         stage('Deploy') { 
               steps {
                 sh ''' #! /bin/bash 
                    '''
                }
            }

         stage('status'){
                steps {
                sh ''' #! /bin/bash
                echo Deployment started
                '''
                }  
            }

        }
        post { 
            always { 
                echo 'Stage is success'
            }
        }    
    }
