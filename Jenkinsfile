pipeline{
  agent { label 'vps-ssh' }

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub_id')
	}

	stages {
		stage('gitclone') {
			steps {
				git branch: 'main', url: 'https://github.com/ByDena9/apache-dockerfile.git'
			}
		}
		stage('Build') {

			steps {
				sh 'sudo docker build -t marcodena/apachemarcos:latest .'
			}
		}

		stage('Login') {
			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {
			steps {
				sh 'sudo docker push marcodena/apachemarcos:latest'
			}
		}
	}

	post {
		always {
			sh 'sudo docker logout'
		}
	}

}
