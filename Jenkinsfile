pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "lukadimi321/kiii-jenkins-pipeline"
        GITHUB_REPO  = "https://github.com/Lukadi123/kiii-jenkins-pipeline.git"
    }

    stages {
        stage('Clone repository') {
            steps {
                git branch: 'main',
                    url: "${GITHUB_REPO}"
            }
        }

        stage('Build image') {
            steps {
                script {
                    dockerImage = docker.build("${DOCKER_IMAGE}:${BUILD_NUMBER}")
                }
            }
        }

        stage('Push image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub-credentials') {
                        dockerImage.push("${BUILD_NUMBER}")
                        dockerImage.push("latest")
                    }
                }
            }
        }
    }
}
