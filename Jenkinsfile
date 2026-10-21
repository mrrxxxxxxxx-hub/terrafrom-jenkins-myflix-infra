pipeline {
    agent {
        docker {
            image 'hashicorp/terraform:latest'
            args '--entrypoint='
        }
    }
    // All AWS credentials save here
    environment {
            AWS_ACCESS_KEY_ID = credentials('AWS_ACCESS_KEY_ID')
            AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
            DB_PASSWORD = credentials('DB_PASSWORD')
    // TFVARS ADDED 
            TF_VAR_AWS_ACCESS_KEY_ID = credentials('AWS_ACCESS_KEY_ID')
            TF_VAR_AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
            TF_VAR_DB_PASSWORD = credentials('DB_PASSWORD')
    }        


     stages {
        stage('Terraform Init') {
            steps {
                echo 'terraform init is starting'
                sh 'terraform init'
            }
        }

        stage('Terraform Plan') {
            steps {
                echo 'Terraform Plan is starting'
                sh 'terraform plan'
            }
        }

        stage('Approval Button') {
            steps {
                input message: 'Please check your terraform plan', ok: 'proceed'
            }
        }

        stage('Terraform Destroy') {
            steps {
                echo 'Terraform destroy is running'
                sh 'terraform destroy -auto-approve'
            }
        }
    }
}                                                                   