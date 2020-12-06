@Library('shared-lib')_


pipeline {
agent any 

stages {
 stage ("Build image") {
       steps {
             script{
                   try {
                       def dockerDetails = readJSON file: "${env.WORKSPACE}/docker-details.json"
                       dockerBuild(dockerDetails.docker_user)
                       }
                   catch(Exception err)
    					{
        					
						error "Docker build failed due to ${err}"
    					}
                   }
             }
       }
  stage ("Push image to Docker registry") {
         steps {
             script{
                   try {
                       dockerPush()
                       }
                   catch(Exception err)
    					{
        					
						error "Docker image push failed due to ${err}"
    					}
                   }
             }
   }
  stage ("Pull latest image from Registry") {
        steps {
             script{
                   try {
                       dockerPull()
                       }
                   catch(Exception err)
    					{
        					
						error "Docker image pull failed due to ${err}"
    					}
                   }
             }
  }
  stage ("Deploy") {
        steps {
             script{
                   try {
                       def dockerDetails = readJSON file: "${env.WORKSPACE}/docker-details.json"
                       dockerDeploy(dockerDetails.docker_user,dockerDetails.external_port,dockerDetails.internal_port)
                       }
                   catch(Exception err)
    					{
        					
						error "Docker deploying of container failed due to ${err}"
    					}
                   }
             }
         }
   }
} 
