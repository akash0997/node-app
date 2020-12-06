@Library('shared-lib')_


pipeline {
agent any 

stages {
 stage ("Build") {
       steps {
             dockerBuild()
            //sh 'docker build -t akash97/${JOB_NAME}:${BUILD_NUMBER} .';
            //sh 'docker tag akash97/${JOB_NAME}:${BUILD_NUMBER} akash97/${JOB_NAME}:latest'
            //sh 'docker images'
             }
       }
  stage ("Push to Docker registry") {
         steps {
            withCredentials([usernamePassword(credentialsId: 'docker-cred', passwordVariable: 'pass', usernameVariable: 'usr')]){
            dockerPush($usr,$pass)
            // sh '''
            //     docker login --username ${usr} --password ${pass}
            //     docker push akash97/${JOB_NAME}:${BUILD_NUMBER}
            //     docker push akash97/${JOB_NAME}:latest
            //  '''
       }       
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
            //  sh '''
            //      container_id=$(docker ps -qf "name=${JOB_NAME}") && [ -z $container_id ] && echo "Container not running" || (docker stop $container_id && docker rm $container_id)
            //      docker run -p 5000:8000 --name ${JOB_NAME} -d akash97/${JOB_NAME}:latest
            //     '''            
               }
           }
     }
} 
