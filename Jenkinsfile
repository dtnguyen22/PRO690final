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
				sh 'docker build -t ubnd/node-app:latest .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push ubnd/node-app:latest'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}
