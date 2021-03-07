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
       sh "docker ps"
       def imageExists=sh("docker ps | grep 8080 | wc -l")
       echo "imageExists: $imageExists"
       if (!imageExists) 
       {
       sh "docker run -d -p 8084:8080 dockertestkumar/docker_proj"
       sh "docker ps"     
       }             
       sh "curl -k http://localhost:8084/dockerdemo"      
            }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker ps"  
                sh "docker -H ssh://jenkins@18.222.253.78 run -d -p 8084:8080 dockertestkumar/docker_proj"
                sh "docker ps"  
            }
        }
    }
 }
