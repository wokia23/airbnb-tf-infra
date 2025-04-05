def COLOR_MAP = [
    'SUCCESS': 'good',
    'FAILURE': 'danger',
    ]

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
                echo 'testing jenkins pipeline'
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

    post {
        success {
            echo 'fantastic job, send build result'
            slackSend channel: "#et-devops-team", color: COLOR_MAP[currentBuild.currentResult], message: "Build Started by wokia: ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)"
        }
    }
}
