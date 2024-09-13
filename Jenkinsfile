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
                    docker.build('my-terraform-image')
                    
                    // List Docker images for debugging
                    sh 'docker images'
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://registry-1.docker.io/', 'docker-hub-credentials') {
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


pipeline {
    agent {
        docker {
            image 'my-terraform-image' // Use the Docker image created
            label 'docker' // Optional if using Docker-based Jenkins agents
        }
    }
    stages {
        stage('Terraform Init') {
            steps {
                sh 'terraform init'
            }
        }
        stage('Terraform Plan') {
            steps {
                sh 'terraform plan'
            }
        }
        stage('Terraform Apply') {
            steps {
                sh 'terraform apply -auto-approve'
            }
        }
    }
    post {
        success {
            echo 'Terraform apply was successful!'
        }
        failure {
            echo 'Terraform apply failed.'
        }
    }
}

