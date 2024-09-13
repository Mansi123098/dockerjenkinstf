pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    def customImage = docker.build('my-terraform-image')
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub-credentials') {
                        // Define the full image name
                        def imageName = 'mansinair/my-terraform-image'
                        
                        // Tag the built image
                        docker.image('my-terraform-image').tag("${imageName}:latest")
                        
                        // Push the tagged image to Docker Hub
                        docker.image("${imageName}:latest").push('latest')
                    }
                }
            }
        }
    }
}
