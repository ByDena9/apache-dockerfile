pipeline{
  agent { label 'vps-ssh' }

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub_id')
	}

	stages {
		stage('gitclone') {
			steps {
				git 'https://github.com/raulmoes/apache-dockerfile.git'
				sh 'cd apache-dockerfile'
			}
		}
		stage('Build') {

			steps {
				sh 'sudo docker build -t apacheraul/apacheraul:latest .'
			}
		}

		stage('Login') {
			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {
			steps {
				sh 'sudo docker push apacheraul/apacheraul:latest'
			}
		}
	}

	post {
		always {
			sh 'sudo docker logout'
		}
	}

}
