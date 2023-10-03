// //script

// node {
// 	echo "Buiid"
// 	echo "Test"
// 	echo "Integration Test"
	
// }

//declarative

pipeline {
	agent any
	// agent { docker {image 'maven:3.6.3'} }
	// agent { docker {image 'node:13.8'} }
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven' 
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"

	}


	stages {
		stage('Checkout') {
			steps {
				sh "mvn --version"
				sh "docker version"
				echo "Buiid"
				echo "PATH - $PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"
			}
		}

		stage('Compile') {
			steps {
				sh "mvn clean compile"
				sh "mvn package -DskipTests"
			}
		}

		stage('Build Docker image') {
			steps {
				// "docker build -t track777/currency-exchange-azure-devops:$env.BUILD_TAG"
				script {
					dockerImage = docker.build("track777/currency-exchange-azure-devops:${$env.BUILD_TAG}")
				}
			}
		}

		stage('Push Docker image') {
			steps {
				docker.withRegistry('', 'dockerhub') {
					dockerImage.push();
					dockerImage.push('latest');
				}
		
			}
		}
		
		// stage('Test') {
		// 	steps {
		// 		sh "mvn test"
		// 	}
		// }
		

		
		// stage('Integration Test') {
		// 	steps {
		// 		echo "mvn failsafe:integration-test failsafe:verify"
		// 	}
		// }
		
	} 
	post {
		always {
			echo "I run always"
		}
		success {
			echo "i am success"
		}
		failure {
			echo "make failure"
		}
		// changed 
	}
	
}
