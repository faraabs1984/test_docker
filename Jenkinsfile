pipeline {
    agent any
	
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/faraabs1984/test_docker.git'
             
          }
        }
	
        

  stage('Docker Build and Tag') {
           steps {
              	echo "==============Start building docker image============="
                sh 'docker build -t test_docker:latest .' 
                sh 'docker tag test_docker faraabs/test_docker:latest'
                //sh 'docker tag samplewebapp nikhilnidhi/samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
		   echo "==============Start pushing docker image to hub.docker.com ============="
        withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
          sh  'docker push faraabs/test_docker:latest'
        //  sh  'docker push nikhilnidhi/samplewebapp:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps {
		   echo "==============Start running docker container============="
                sh "docker run -d -p 8888:80 faraabs/test_docker"
 
            }
        }
 }
}
    
