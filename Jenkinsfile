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
       script
       {
       sh "docker ps"
       def imageExists=sh(script: "docker ps | grep 8080 | wc -l", returnStdout: true).trim()
       echo "imageExists: $imageExists"
       if (imageExists=="0") 
       {
       sh "docker run -d -p 8084:8080 dockertestkumar/docker_proj"
       sh "docker ps"     
       }
       sh "nslookup localhost"
     //  sh "curl http://localhost:8084/Dockerdemo"      
       }
                  }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker ps"  
                sh "docker -H ssh://root@34.82.30.166 run -d -p 8085:8080 dockertestkumar/docker_proj"
                sh "docker ps"  
            }
        }
    }
 }
