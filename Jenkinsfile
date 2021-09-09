node{
   stage('SCM Checkout'){
       git branch: 'main', credentialsId: 'git-cred', url: 'https://github.com/vasantharajksks/Multibranch-jenkins-spring-boot.git'
   }
   stage('Mvn Package'){
     def mvnHome = tool name: 'maven-3', type: 'maven'
     def mvnCMD = "${mvnHome}/bin/mvn"
     sh "${mvnCMD} clean package"
   }
   stage('Build Docker Image'){
     sh 'docker build -t my-app .'
   }
   
    stage('Run Container on Server'){
     sh 'docker run -p 8080:8080 -d --name my-app my-app'
    }
       
}
