pipeline {
    agent {
        docker {
            image 'hashicorp/terraform' // Use the desired Terraform Docker image
            args  '--entrypoint=""'          // Override the default entrypoint if necessary
        }
    }
    


    stages {


        stage('Terraform Init') {
            steps {
                script {
                    // Run terraform init
                    sh 'terraform init'
                }
            }
        }

        

        
    }

    post {
        always {
            // Archive Terraform plan files or other artifacts if needed
            archiveArtifacts artifacts: 'terraform.plan', allowEmptyArchive: true
        }

        success {
            echo 'Terraform scripts executed successfully!'
        }

        failure {
            echo 'Terraform scripts failed!'
        }
    }
}
