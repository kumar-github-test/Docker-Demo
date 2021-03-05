pipeline {
    agent any
 
   tools
    {
       maven "Maven"
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
 }
}
