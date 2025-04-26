pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'yash11526512/node-app:latest'
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build(DOCKER_IMAGE)
                }
            }
        }
        stage('Push to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-creds', url: 'https://index.docker.io/v1/']) {
                    script {
                        docker.image(DOCKER_IMAGE).push()
                    }
                }
            }
        }
    }
}
