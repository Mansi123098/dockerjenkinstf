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

        
    }

    post {
        always {
            // Clean up workspace or perform other post-build actions
            cleanWs()
        }
    }
}
