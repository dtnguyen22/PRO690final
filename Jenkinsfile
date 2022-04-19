pipeline{

	agent {
			//use agent1 node for jobs
        	node {
            		label 'agent1'
        		}
    		}


	environment {
		//dockerhub-creds is stored in jenkins credentials
		DOCKERHUB_CREDENTIALS=credentials('dockerhub-creds')
	}

	stages {

		stage('Build') {
			//builds docker image, uses build_id for tag
			steps {
				sh 'docker build -t ubnd/node-app:$BUILD_ID .'
			}
		}

		stage('Login') {
			//logs in dockerhub
			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {
			//push the newly built image to dockerhub
			steps {
				sh 'docker push ubnd/node-app:$BUILD_ID'
			}
		}
	}
	//logout
	post {
		always {
			sh 'docker logout'
		}
	}

}
