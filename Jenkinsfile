pipeline{
	agent any
	//agent { docker { image 'maven:3.6.3' } }
	//agent { docker { image 'node:13.8' } }
    environment{
		dockerHome =  tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}

	stages{
		stage('Build'){
			steps{
				sh 'mvn --version' 
				sh 'docker version'
				//sh 'node --version'
				echo 'Build'
			}
		}
		stage('Test'){
			steps{
				echo 'Test'
			}
		}
		stage('Integration Test'){
			steps{
				echo 'Integration Test'
			}
		}
	} 
	
	post {
		always{
			echo 'Ill Always run'
		}
		success{
			echo 'I run when you are successful'
		}
		failure{
			echo 'I run when you are fail'
		}
	}
	
}