// //script

// node {
// 	echo "Buiid"
// 	echo "Test"
// 	echo "Integration Test"
	
// }

//declarative

pipeline {
	// agent any
	// agent { docker {image 'maven:3.6.3'} }
	agent { docker {image 'node:13.8'} }
	stages {
		stage('Build') {
			steps {
				// sh "mvn --version"
				sh "node --version"
				echo "Buiid"
			}
		}
		
		stage('Test') {
			steps {
				echo "Test"
			}
		}
		
		stage('Integration Test') {
			steps {
				echo "Integration Test"
			}
		}
		
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
