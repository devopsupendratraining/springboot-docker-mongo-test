pipeline{


agent any
 
 tools{
   maven 'maven 3.6.3'
 }
 
 
 stages{
 
   stage("Git Checkout"){
      steps{
	      
       git credentialsId: '8081002c-b145-4930-89e6-6da5a0bb598d', url: 'https://github.com/devopsupendratraining/springboot-docker-mongo-test.git'
	     // https://<USERNAME>:<PASSWORD>@github.com/path/to/repo.git
      }
    }
    
    stage("mvn build"){
			steps{
			  sh "mvn clean package"
			}
	}
  
   stage("docker image build"){
			steps{
				sh "docker build -t  ragula001/springboot-mongo-docker:${BUILD_NUMBER} . "
				
			}
	}
  
  stage("docker image push to docker rep"){
			steps{
			
				withCredentials([string(credentialsId: 'dock_hub_pwd', variable: 'docker_hub_pwd')]) {
					sh "docker login -u ragula001 -p ${docker_hub_pwd}"
				}
				sh "docker push ragula001/springboot-mongo-docker:${BUILD_NUMBER}"  
				
			}
	}
	  
		  stage("run docker image in container"){
					steps{

						sshagent(['dockerun']) {
							sh 'scp -o StrictHostKeyChecking=no  docker-compose.yml ubuntu@15.207.16.144:'
							sh 'ssh ubuntu@15.207.16.144 docker-compose up -d'
						}

					}
			}

	 
  
  
 
 
 
 
 }

}
