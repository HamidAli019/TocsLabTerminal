pipeline {
    agent any

    environment {
        DOCKER_HUB_CREDENTIALS = credentials('docker-hub-credentials-id')
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/HamidAli019/TocsLabTerminal.gits'
            }
        }

        stage('Build') {
            steps {
                script {
                    docker.build('docker-image:latest')
                }
            }
        }

        stage('Test') {
            steps {
                // Implement your testing steps here
            }
        }

        stage('Deploy') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'DOCKER_HUB_CREDENTIALS') {
                        docker.image('docker-image:latest').push()
                    }
                }
            }
        }
    }

    post {
        failure {
            echo 'Rollback to the previous version'
        }

        unstable {
            emailext (
                subject: 'Build Unstable: ${currentBuild.fullDisplayName}',
                body: 'The build is unstable.',
                recipientProviders: [culprits()]
            )
        }

        success {
            emailext (
                subject: 'Build Successful: ${currentBuild.fullDisplayName}',
                body: 'The build and deployment were successful.',
                recipientProviders: [culprits()]
            )
        }
    }
}
