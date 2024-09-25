pipeline {
    agent any
    
    environment {
        DOCKER_HUB_REPO = 'i211221/mlopstask3'
        DOCKER_HUB_CREDENTIALS_ID = '1221'
        //Image Tag
        IMAGE_TAG = "${env.BUILD_ID}"
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_HUB_REPO}:${IMAGE_TAG}")
                }
            }
        }

        stage('Login to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_HUB_CREDENTIALS_ID) {
                        echo "Logged in successfully"
                    }
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.image("${DOCKER_HUB_REPO}:${IMAGE_TAG}").push()
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
