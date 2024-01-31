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
		stage('Checkout'){
			steps{
				sh 'mvn --version' 
				sh 'docker version'
				//sh 'node --version'
				echo 'Build'
				//Jenkind has many global environmental variables - some examples
				echo "PATH - $PATH"
				echo "BUILD_NUMBER - $BUILD_NUMBER"
				echo "BUILD_ID - $BUILD_ID"
				echo "JOB_NAME - $JOB_NAME"
				echo "BUILD_TAG - $BUILD_TAG"
				echo "BUILD_URL - $BUILD_URL"
			}
		}
		stage('Compile'){
			steps{
				sh 'mvn clean compile'
			}
		}
		stege('Package'){
			steps{
				sh 'mnv package -DskipTests'
			}
		}
		stage('Build Docker Image'){
			steps{
				//docker build -t vishnuvarthan2701/currency-exchange-devops:$BUILD_TAG
				script{
					dockerImage = docker.build("vishnuvarthan2701/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}
		stage('Push Docker Image'){
			steps{
				script{
					docker.withRegistry('','dockerhub'){
						dockerImage.push()
						dockerImage.push('latest')
					}
				}
			}
		}

		//commenting due to version error
		// stage('Test'){
		// 	steps{
		// 		sh 'mvn test'
		// 	}
		// }
		// stage('Integration Test'){
		// 	steps{
		// 		sh 'mvn failsafe:integration-test failsafe:verify'
		// 	}
		// }
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