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
              
                sh 'docker build -t test_docker:latest .' 
                sh 'docker tag test_docker faraabs/test_docker:latest'
                //sh 'docker tag samplewebapp nikhilnidhi/samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
          sh  'docker push faraabs/test_docker:latest'
        //  sh  'docker push nikhilnidhi/samplewebapp:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8003:8080 faraabs/test_docker"
 
            }
        }
 }
}
    
