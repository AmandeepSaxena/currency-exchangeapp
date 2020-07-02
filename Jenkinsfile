pipeline{
	agent any
	environment{
		dockerHome = tool 'Docker'
		mavenHome = tool 'Maven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages{
		stage("Checkout"){
			steps{
				echo "Build"
				echo "Path - $PATH"	
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"	
				echo "BUILD_ID - $env.BUILD_ID"	
				echo "JOB_NAME - $env.JOB_NAME"	
				echo "BUILD_TAG - $env.BUILD_TAG"	
				echo "BUILD_URL - $env.BUILD_URL"	
				sh  'docker version'
			}
		}
		stage('Compile'){
			steps{
				sh 'mvn clean compile'   
			}	
		}
		stage('Test'){
			steps{
				sh 'mvn test'
			}
		}
		stage('Integration Test'){
			steps{
				sh 'mvn failsafe:integration-test failsafe:verify'
			}
		}
		stage('Build Docker Image'){
			steps{
				dockerImage = docker.build('noobaman/currency-exchangeapp:${env.BUILD_TAG}')
			}
		}
		stage('Push Docker Image'){
			steps{
				docker.withRegistry('','dockerhub'){
					dockerImage.push();
					dockerImage.push('latest')
				}
			}
		}
	}
	
}