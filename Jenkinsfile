pipeline {
    agent any

    stages {
        stage('npm') {
            agent {
                docker {
                    image 'node:18'
                    args '--entrypoint=""'
                }
            }
            steps {
                  script {
                    // Run a simple hello command
                    sh 'echo "Hello, World!"'
                    
                    // Optionally install npm packages or run npm commands
                    // sh 'npm install'
                    // sh 'npm run my-script'
                }
              }
        }

        stage('Run Terraform') {
            agent {
                docker {
                    image 'terraform-image:latest'
                    args '--entrypoint=""'
                }
            }
            steps {
                script {
                    sh 'terraform init'
                    echo 'completed'
                }
            }
        }
    }

    post {
        always {
            // Clean up workspace or perform other post-build actions
            cleanWs()
        }
    }
}
