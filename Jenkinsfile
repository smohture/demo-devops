pipeline {
    agent any
    tools{
        maven "3.8.5"
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/smohture/demo-devops']])
                sh 'mvn clean install'

            }
        }
        stage('Build Docker Image'){
            steps{
                script{
                    sh 'docker build -t shubhammohture/devops-integration .'
                }
            }
        }
        stage('push image to docker hub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerpwd', variable: 'dockerpwd')]) {
                        sh 'docker login -u shubhammohture -p ${dockerpwd}'
                    }
                    sh 'docker push shubhammohture/devops-integration'
                }
            }
        }
    }
}