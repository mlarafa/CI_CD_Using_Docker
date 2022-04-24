pipeline { 
	agent any 
	tools 
	{ 
		maven "Maven" 
	} 
	stages { 
		stage('checkout') { 
			steps { 
				git branch: 'master', url: 'https://github.com/jmalahmad/CI_CD_Using_Docker.git' 
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
				// sh 'docker tag samplewebapp jmlhmd/samplewebapp:latest' 
				//sh 'docker tag samplewebapp jmlhmd/samplewebapp:$BUILD_NUMBER' 
			} 
		} 
		stage('Publish image to Docker Hub') { 
			steps { withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) { 
				sh 'docker push jmlhmd/samplewebapp:latest' 
				// sh 'docker push jmlhmd/samplewebapp:$BUILD_NUMBER' 
			} 
		} 
		} 
		stage('Run Docker container on Jenkins Agent') { 
			steps { 
				sh "docker run -d -p 8003:8080 jmlhmd/samplewebapp" 
			} 
		} 
	} 
}
