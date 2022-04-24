pipeline { 
	agent any 
	tools 
	{ 
		maven "apache maven 3.8.5" 
	} 
	stages { 
		stage('checkout') { 
			steps { 
				git branch: 'master', url: 'https://github.com/mlarafa/CI_CD_Using_Docker.git' 
			} 
		} 
		stage('Execute Maven') { 
			steps { 
				sh 'mvn package' 
			} 
		} 
		stage('Docker Build and Tag') { 
			steps { 
				sh 'docker build -t samplewebapp:latest .' 
				// sh 'docker tag samplewebapp mlarafa/samplewebapp:latest' 
				//sh 'docker tag samplewebapp mlarafa/samplewebapp:$BUILD_NUMBER' 
			} 
		}  
		stage('Run Docker container on Jenkins Agent') { 
			steps { 
				sh "docker run -d -p 8003:8080 samplewebapp" 
			} 
		} 
	} 
}
