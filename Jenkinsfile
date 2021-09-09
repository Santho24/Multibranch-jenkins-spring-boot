node{
   stage('SCM Checkout'){
       git branch: 'dev', credentialsId: 'git-cred', url: 'https://github.com/vasantharajksks/Multibranch-jenkins-spring-boot.git'
   }
   stage('Mvn Package'){
     def mvnHome = tool name: 'maven-3', type: 'maven'
     def mvnCMD = "${mvnHome}/bin/mvn"
     sh "${mvnCMD} clean package"
   }
   stage('Build Docker Image'){
     sh 'docker build -t my-app-dev .'
   }
   
    stage('Run Container on Server'){
     sh 'docker run -p 8080:8082 -d --name my-app-dev my-app-dev'
    }
       
}
