pipeline {
agent any 

stages {
 stage ("Build") {
       steps {
            sh 'docker build -t akash97/${JOB_NAME}:${BUILD_NUMBER} .';
            sh 'docker tag akash97/${JOB_NAME}:${BUILD_NUMBER} akash97/${JOB_NAME}:latest'
            sh 'docker images'
             }
       }
  stage ("Push to Docker registry") {
         steps {
            sh 'docker push akash97/${JOB_NAME}:${BUILD_NUMBER}'
            sh 'docker push akash97/${JOB_NAME}:latest'
     }
   }
  stage ("Pull latest image") {
        steps {
            sh 'docker pull akash97/${JOB_NAME}:latest'
              }
          }
  stage ("Deploy") {
        steps {
             sh 'container_id=$(docker ps -qf "name=${JOB_NAME}") && [ -z "$container_id" ] && echo 'Container not running' || docker stop "$container_id"'
             sh 'docker run -p 5000:8000 --name ${JOB_NAME} -d akash97/${JOB_NAME}:latest'
              }
           }
     }
} 
