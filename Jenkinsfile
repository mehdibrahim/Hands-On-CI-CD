pipeline {

    agent any

    tools{
        maven 'maven_3_5_0'
    }
    stages{
        stage ('Build Maven'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/mehdibrahim/devops-automation']])
                sh 'mvn clean install'
            }
        }
        stage ('Build Docker Image'){
            steps{
                
                script{
                    sh 'docker build -t mehdibrahim/devops-integration .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerHubPwd')]) {
                sh 'docker login -u mehdibrahim -p ${dockerHubPwd}'
                sh 'docker push mehdibrahim/devops-integration'
                    
               }
            }
        }
    }
}