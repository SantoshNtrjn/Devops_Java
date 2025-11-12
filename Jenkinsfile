pipeline {
    agent any
    tools {
        maven 'Maven' // Assumes you have a Maven tool configured in Jenkins Global Tool Configuration
    }
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')
        DOCKER_IMAGE_NAME = "santoshntrjn/devops-java"
        DOCKER_IMAGE_TAG = "latest"
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build(DOCKER_IMAGE_NAME, ".")
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', DOCKERHUB_CREDENTIALS) {
                        docker.image(DOCKER_IMAGE_NAME).push(DOCKER_IMAGE_TAG)
                    }
                }
            }
        }
    }
}
