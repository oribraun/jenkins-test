pipeline {
	environment {
		imagename = "deploy-test"
		registryCredential = 'yenigul-dockerhub'
		dockerImage = ''
	}
    agent any
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
            steps{
                script{
                    dockerImage = docker.build imagename + ":$BUILD_NUMBER"
                }
            }

        }
    }
}