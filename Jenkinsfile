node{
   stage('SCM Checkout'){
        git 'https://github.com/vijayakumari2496/my-app.git'
   }
   stage('Maven-build'){
      def mvnHome =  tool name: 'maven3', type: 'maven'   
      sh "${mvnHome}/bin/mvn package"
	  sh 'mv target/myweb*.war target/newapp.war'
   }
   stage('Build Docker Image'){
   sh 'docker build -t vijayamalini2496/myweb .'
   }
   stage('Docker Image Push'){
   withCredentials([string(credentialsId: 'dockerPass', variable:'dockerPassword')]) {
   sh "docker login -u vijayamalini2496 -p ${dockerPassword}"
   sh 'docker push vijayamalini2496/myweb'
   }
}
   stage('Docker deployment'){
   sh 'docker run -d -p 8090:8080 --name tomcattest vijayamalini2496/myweb' 
   }
}
