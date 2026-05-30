pipeline {
    agent any
    environment { 
        PATH = "/opt/homebrew/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin" 
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                url: 'https://github.com/dileenaparappalli/MyTerraformPracticeRepo.git'
            }
        }

        stage('Terraform Init') {
            steps {
                sh 'terraform init'
                echo 'init completed'
            }
        }

        stage('Terraform Validate') {
            steps {
                sh 'terraform validate'
                echo 'validate done'
            }
        }

        stage('Terraform Plan') {
            steps {
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws-credentials'
                ]]) {

                    sh 'terraform plan'
                }
            }
        }

        stage('Terraform Apply') {
            steps {
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws-credentials'
                ]]) {

                    sh 'terraform apply --auto-approve'
                }
            }
        }
    }
}
