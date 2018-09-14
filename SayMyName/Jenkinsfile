pipeline {
    agent any
    stages {
        stage('prepare') {
            steps {
                echo 'Cloning repository'
                git 'https://github.com/chufty/aws-lambda-shout.git'
                
                echo 'Restoring packages'
                sh 'dotnet restore'
                
                sh 'dotnet clean'
            }
        }
        
        stage('build') {
            steps {
                echo 'Building solution'
                sh 'dotnet build --configuration Release'
            }
        }
        
        stage('test') {
            steps {
                echo 'There are no tests...'
            }
        }
        
        stage('deploy') {
            steps {
                echo 'Deploying to AWS'
                dir('SayMyName') {
                    withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'AWS_LAMBDA_DEPLOY_CREDENTIALS']]) {
                        sh 'dotnet lambda deploy-function ShoutMe'
                    }
                }
            }
        }
    }
}