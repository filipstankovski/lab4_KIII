pipeline {
    agent any

    environment {
        IMAGE_NAME = "my-image"
    }

    stages {
        stage('Clone repository') {
            steps {
                echo 'Repository cloned by Jenkins automatically'
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
