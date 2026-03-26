pipeline {
    agent {
        docker {
            image 'docker:latest'
            args '--privileged'
        }
    }

    environment {
        IMAGE_NAME = "my-image"
    }

    stages {
        stage('Clone repository') {
            steps {
                echo 'Repository cloned'
            }
        }

        stage('Build image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Push image') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-creds',
                    usernameVariable: 'DOCKER_USERNAME',
                    passwordVariable: 'DOCKER_PASSWORD'
                )]) {
                    sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                    sh 'docker push $IMAGE_NAME'
                }
            }
        }
    }
}
