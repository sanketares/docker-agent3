pipeline {
    agent {
        docker {
            image 'hashicorp/terraform' // Use the desired Terraform Docker image
            args  '--entrypoint=""'          // Override the default entrypoint if necessary
        }
    }


    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/sanketares/docker-agent3.git'
            }
        }

        stage('Terraform Init') {
            steps {
                script {
                    // Run terraform init
                    sh 'terraform init'
                }
            }
        }

        stage('Terraform Plan') {
            steps {
                script {
                    // Run terraform plan
                    sh 'terraform plan'
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
