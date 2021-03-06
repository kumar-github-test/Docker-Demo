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
                sh 'docker tag proj3 dockertestkumar/docker_proj:latest'
                               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerhub", url: "" ]) {
          sh  'docker push dockertestkumar/docker_proj:latest'        
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
   {
                sh "docker run -d -p 8084:8080 dockertestkumar/docker_proj"
 
            }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh://jenkins@52.152.224.93 run -d -p 8084:8080 dockertestkumar/docker_proj"
 
            }
        }
    }
 }
