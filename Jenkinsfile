pipeline {
    agent any

    environment {
        IMAGE_NAME = "1ms24mc102/nodejs-app:latest"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git 'https://github.com/1ms24mc102/nodejs-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Push Image to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'dockerHub']) {
                    sh 'docker push $IMAGE_NAME'
                }
            }
        }

        stage('Deploy to Docker Swarm') {
            steps {
                sh 'docker stack deploy -c docker-stack.yml nodeapp'
            }
        }
    }
}
