pipeline {

	environment {
    registry = '701831127635.dkr.ecr.eu-west-1.amazonaws.com/myapp'
    registryCredential = 'AWS_JENKINS_CREDENTIALS'
    dockerImage = ''
    }

	agent any

	stages {
		stage('Build Dokcer image'){
			steps {
				script {

					dockerImage = docker.build registry + ":$BUILD_NUMBER"
				}
			}
		}
		stage('Deploy image'){
			steps {
				script {
					docker.withRegistry("https://" + registry, "ecr:eu-west-1:" + registryCredential){
						dockerImage.push()
					}
				}
			}
		}
	}
}