pipeline {
    agent any
 
    tools {
        maven 'Maven'
    }
 
    environment {
        // CORRECTED: Added '=' sign to define the variable
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')
 
        // CORRECTED: Added '=' signs and fixed variable name format
        DOCKER_IMAGE_NAME = "santoshntrjn/devops-java"
        DOCKER_IMAGE_TAG  = "latest"
    }
 
    stages {
        // CORRECTED: 'steps' instead of 'stepa'
        stage('Build with Maven') {
            steps {
                sh 'mvn clean package' // Use 'package' for this simple project
            }
        }
 
        stage('Build Docker Image') {
            steps {
                script {
                    // CORRECTED: Using the proper variable name DOCKER_IMAGE_NAME
                    docker.build(DOCKER_IMAGE_NAME, ".")
                }
            }
        }
 
        stage('Push Docker Image') {
            steps {
                script {
                    // CORRECTED: Using the proper variable names
                    docker.withRegistry('https://registry.hub.docker.com', DOCKERHUB_CREDENTIALS) {
                        docker.image(DOCKER_IMAGE_NAME).push(DOCKER_IMAGE_TAG)
                    }
                }
            }
        }
    }
}
