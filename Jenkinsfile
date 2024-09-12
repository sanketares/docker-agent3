pipeline {
    agent {
        docker {
            image 'hashicorp/terraform:1.5.0' // Use the desired Terraform Docker image
            args  '--entrypoint=""'          // Override the default entrypoint if necessary
        }
    }


    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: ''
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

        stage('Terraform Apply') {
            steps {
                script {
                    // Run terraform apply
                    // Note: The `-auto-approve` flag is used here to automatically approve the apply action.
                    sh 'terraform apply -auto-approve'
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
