pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'yash11526512/node-app:latest'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/Yash-Khandal/Iac_Test.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}", ".") // build from current directory
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withDockerRegistry([ credentialsId: 'docker-hub-creds', url: '' ]) {
                    script {
                        docker.image("${DOCKER_IMAGE}").push()
                    }
                }
            }
        }
    }
}
