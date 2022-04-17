pipeline{

	agent {
        	node {
            		label 'agent1'
        		}
    		}


	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub-creds')
	}

	stages {

		stage('Build') {

			steps {
				sh 'docker build -t ubnd/node-app:$BUILD_ID .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push ubnd/node-app:$BUILD_ID'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}
