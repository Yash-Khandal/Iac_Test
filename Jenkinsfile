pipeline {
    agent any

    environment {
        // Use a dynamic tag (BUILD_ID is available by default in Jenkins)
        DOCKER_IMAGE = 'yash11526512/node-app'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main', 
                url: 'https://github.com/Yash-Khandal/Iac_Test.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Explicitly specify the directory containing Dockerfile
                    docker.build("${DOCKER_IMAGE}:${env.BUILD_ID}", "./node-app")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-creds', url: 'https://registry.hub.docker.com']) {
                    script {
                        // Push both the build-specific tag and latest
                        docker.image("${DOCKER_IMAGE}:${env.BUILD_ID}").push()
                        docker.image("${DOCKER_IMAGE}:${env.BUILD_ID}").push('latest')
                    }
                }
            }
        }
    }

    post {
        success {
            echo "Successfully pushed ${DOCKER_IMAGE}:${env.BUILD_ID} to Docker Hub"
        }
        failure {
            echo "Pipeline failed - check the logs for errors"
        }
    }
}
