node{
   stage('SCM Checkout'){
     git 'https://github.com/jayaveeran13/my-app.git'
   }
   stage('maven-buildstage'){

      def mvnHome =  tool name: 'maven', type: 'maven'   
      sh "${mvnHome}/bin/mvn clean package"
	  sh 'mv target/myweb*.war target/newapp.war'
   }
    stage('SonarQube Analysis') {
	        def mvnHome =  tool name: 'maven', type: 'maven'
	        withSonarQubeEnv('sonar') { 
	          sh "${mvnHome}/bin/mvn sonar:sonar"
	        }
	    }
   stage('Build Docker Image'){
   sh 'docker build -t jayaveeran13/myweb:0.0.2 .'
   }
   stage('Docker Image Push'){
   withCredentials([string(credentialsId: 'dockerPass', variable: 'dockerPassword')]) {
   sh "docker login -u jayaveeran13 -p ${dockerPassword}"
    }
   sh 'docker push jayaveeran13/myweb:0.0.2'
   }
  stage('Nexus Image Push'){
   sh "docker login -u admin -p admin123 54.172.29.176:8083"
   sh "docker tag jayaveeran13/myweb:0.0.2 54.172.29.176:8083/jay:1.0.0"
   sh 'docker push 54.172.29.176:8083/jay:1.0.0'
   }

   stage('Remove Previous Container'){
	try{
		sh 'docker rm -f tomcattest'
	}catch(error){
		//  do nothing if there is an exception
	}
   stage('Docker deployment'){
   sh 'docker run -d -p 8090:8080 --name tomcattest jayaveeran13/myweb:0.0.2' 
   }
   }
}
