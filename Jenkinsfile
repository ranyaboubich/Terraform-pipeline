pipeline {
    agent any

    environment {
        ARM_CLIENT_ID = credentials('azure-client-id')
        ARM_CLIENT_SECRET = credentials('azure-client-secret')
        ARM_SUBSCRIPTION_ID = credentials('azure-subscription-id')
        ARM_TENANT_ID = credentials('azure-tenant-id')
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/ranyaboubich/Hello-world-pipeline'
            }
        }

        stage('Terraform Init') {
            steps {
                script {
                    echo 'Initializing Terraform...'
                    bat 'terraform init'
                }
            }
        }

        stage('Terraform Plan') {
            steps {
                script {
                    echo 'Planning Terraform changes...'
                    bat 'terraform plan'
                }
            }
        }

        stage('Terraform Apply') {
            steps {
                script {
                    echo 'Applying Terraform changes...'
                    bat 'terraform apply -auto-approve'
                }
            }
        }
    }

    post {
        success {
            build job: 'CD-Pipeline'
        }
    }
}