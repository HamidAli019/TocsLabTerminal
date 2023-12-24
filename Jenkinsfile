pipeline{

	agent {label 'linux'}

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
	}

	stages {
	    
	    stage('gitclone') {

			steps {
				git 'https://github.com/HamidAli019/TocsLabTerminal.git'
			}
		}

		stage('Build') {

			steps {
				sh 'docker build -t hamid42358987/question2:latest .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push hamid42358987/question2:latest'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}