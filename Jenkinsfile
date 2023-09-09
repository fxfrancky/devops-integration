pipeline {
    agent any
    tools{
        maven 'maven_3_6_3'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: '5f03f9a9-f98d-4fe2-92fc-700411531b8f', url: 'https://github.com/fxfrancky/devops-integration']])
                sh 'mvn clean install'
            }
        }
        stage('Build Docker image'){
            steps{
                script{
                    sh 'docker build -t fxfrancky/devops-integration .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerHubPwd', variable: 'dockerHubPwd')]) {
                    sh 'docker login -u fxfrancky -p ${dockerHubPwd}'
}
                    sh 'docker push fxfrancky/devops-integration'

                }
            }
        }
    }

}