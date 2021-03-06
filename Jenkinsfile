pipeline {
    agent any
 
   tools
    {
       maven "Maven3.6.3"
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/kumar-github-test/Docker-Demo.git'
             
          }
        }
  stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }
     stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t proj3:latest .' 
                sh 'docker tag proj3 dockertestkumar/proj3:latest'
                               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerhub", url: "" ]) {
          sh  'docker push dockertestkumar/proj3:latest'        
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
   {
                sh "docker run -d -p 8081:8080 dockertestkumar/proj3"
 
            }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh://jenkins@3.18.223.5 run -d -p 8081:8080 dockertestkumar/proj3"
 
            }
        }
    }
 }
