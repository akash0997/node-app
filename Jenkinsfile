@Library('shared-lib')_


pipeline {
agent any 

stages {
 stage ("Build") {
       steps {
             script{
                   try {
                     dockerBuild()
                       }
                   catch(Exception err)
    					{
        					
						echo "Docker build failed due to ${err}"
    					}
                   }
             }
       }
  stage ("Push to Docker registry") {
         steps {
            dockerPush()
     }
   }
  stage ("Pull latest image") {
        steps {
           dockerPull()
              }
          }
  stage ("Deploy") {
        steps {
             dockerDeploy()     
               }
           }
     }
} 
