@Library('shared-lib')_


pipeline {
agent any 

stages {
 stage ("Build image") {
       steps {
             script{
                   try {
                       dockerBuild()
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
                       dockerDeploy()
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
