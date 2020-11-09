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
  
   
	  
		  stage("docker compose for dev"){
					steps{

						sshagent(['dockerun']) {
							sh 'scp -o StrictHostKeyChecking=no  docker-compose.yml  ubuntu@15.207.16.144:'
							sh 'scp -o StrictHostKeyChecking=no   docker-compose-dev.yml ubuntu@15.207.16.144:'
							sh 'ssh ubuntu@15.207.16.144 docker-compose -f docker-compose.yml -f docker-compose-ite.yml up -d'
							//sh 'ssh ubuntu@15.207.16.144 docker-compose up -d'
						}

					}
			}
	 
	 stage("docker compose for ite"){
					steps{

						sshagent(['dockerun']) {
							sh 'scp -o StrictHostKeyChecking=no  docker-compose.yml  ubuntu@13.235.82.132:'
							sh 'scp -o StrictHostKeyChecking=no   docker-compose-ite.yml ubuntu@13.235.82.132:'
							sh 'ssh ubuntu@13.235.82.132 docker-compose -f docker-compose.yml -f docker-compose-ite.yml up -d'
							//sh 'ssh ubuntu@15.207.16.144 docker-compose up -d'
						}

					}
			}
	 
	  stage("docker compose for ite"){
					steps{

						sshagent(['dockerun']) {
							sh 'scp -o StrictHostKeyChecking=no  docker-compose.yml  ubuntu@65.0.181.236:'
							sh 'scp -o StrictHostKeyChecking=no   docker-compose-prod.yml ubuntu@65.0.181.236:'
							sh 'ssh ubuntu@65.0.181.236 docker-compose -f docker-compose.yml -f docker-compose-ite.yml up -d'
							//sh 'ssh ubuntu@15.207.16.144 docker-compose up -d'
						}

					}
			}


 
 }

}
