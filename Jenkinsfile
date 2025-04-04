pipeline {
    agent any
    
    tools {
        terraform 'Terraform'
    }

        environment {
        //Credentials for Prod environment
        AWS_ACCESS_KEY_ID     = credentials('AWS_ACCESS_KEY_ID') 
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
    }
 
    stages {
        stage('SCM Checkout') {
            steps {
                echo 'cloning code base to jenkins server'
                git branch: 'main', credentialsId: '65a810ac-63f0-4edc-aeab-15001fe7af1a', url: 'https://github.com/wokia23/airbnb-tf-infra.git'
                sh 'ls'
            }
        }
        
        stage('terraform init') {
            steps {
                sh 'terraform init'
            }
        }
        
        stage('terraform plan') {
            steps {
                sh 'terraform plan'
            }
        }
        
         stage('terraform action to apply or destroyplan') {
            steps {
                sh 'terraform ${action} --auto-approve'
            }
        }
        
    }
}
