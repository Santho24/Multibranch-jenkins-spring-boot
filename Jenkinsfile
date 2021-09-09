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
     sh 'docker build -t vasanth24/my-app-dev:1.0.0 .'
   }
   stage('Push Docker Image'){
     withCredentials([string(credentialsId: 'docker-pwd', variable: 'dockerHubPwd')]) {
        sh "docker login -u vasanth24 -p ${dockerHubPwd}"
     }
     sh 'docker push vasanth24/my-app-dev:1.0.0'
   }
   stage('Run Container on Dev Server'){
     def dockerRun = 'docker run -p 8080:8080 -d --name my-app-dev vasanth24/my-app-dev:1.0.0'
     sshagent(['dev-server']) {
       sh "ssh -o StrictHostKeyChecking=no ec2-user@35.175.151.177 ${dockerRun}"
     }
   }
     
}
