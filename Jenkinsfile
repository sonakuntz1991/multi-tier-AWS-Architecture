pipeline{
    agent any
    tools {
       terraform 'Terraform'
    }
    stages{
        stage('Git Checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/gospelmike/DevOps'
            }
        }
        stage('Terraform Init'){
            steps{
                sh 'terraform init'
            }
        }
        stage('Terraform Plan'){
            steps{
                sh 'terraform plan'
            }
        }
        stage('Terraform Action'){
            steps{
                echo "Terraform Action is --> ${Action}"
                sh ('terraform ${Action} -auto-approve')
            }
        }
       
    }

}
