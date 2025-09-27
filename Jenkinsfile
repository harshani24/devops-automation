pipeline {
    agent any
    tools {
        maven 'maven_3_9_11'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/harshani24/devops-automation']])
                bat 'mvn clean install'

            }
        }
        stage('Build Docker Image'){
            steps{
                script{
                    bat 'docker build -t harshani24/devops-automation .'
                }
            }
        }
        stage('Push Docker Image to Hub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerh-pwd', variable: 'dockerpwd')]) {
                        bat "docker login -u harshani24 -p %dockerpwd%"
                    }
                    bat 'docker push harshani24/devops-automation'
                }
            }
        }
    }
}