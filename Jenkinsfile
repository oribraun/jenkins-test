pipeline {
	environment {
		imagename = "deploy-test"
		registryCredential = 'yenigul-dockerhub'
		dockerImage = ''
	}
    agent {
        docker {
            image 'node:14-alpine'
            args '-p 3000:3000'
        }
    }
    stages {
        stage('Installing Node') { 
            steps {
                sh 'npm install' 
            }
        }

        stage ('Conducting Unit test'){
            steps{
                sh 'npm test'
            }

        }
		stage ('Building image'){
			agent {
				docker {
					image 'node:14-alpine'
					args '-p 3000:3000'
				}
			}
            steps{
                script{
                    dockerImage = docker.build imagename + ":$BUILD_NUMBER"
                }
            }

        }
    }
}