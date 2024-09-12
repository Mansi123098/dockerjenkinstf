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
                    docker.build('my-terraform-image')
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub-credentials') {
                        docker.image('my-terraform-image').push('latest')
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
