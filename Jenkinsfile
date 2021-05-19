pipeline {
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
            steps{
                script{
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }

        }
		stage ('Pushing to Docker Hub'){
            steps{
                script{
                    docker.withRegistry('',registyCredential){
                        dockerImage.push()
                    }
                }
            }

        }
    }
}