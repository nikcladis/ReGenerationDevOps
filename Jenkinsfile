pipeline {
    agent any

    stages {
        stage('Clone repository') {
            steps {
                git 'https://github.com/nikcladis/toDoAppWithLogin-Regeneration-CyberSecurity-DevOps.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Archive JAR file') {
            steps {
                archiveArtifacts 'target/*.jar'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t nikcladis/app .'
            }
        }
        
        stage('Push Docker Image') {
            steps {
                withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhubpwd')]) {
                sh 'docker login -u nikcladis -p ${dockerhubpwd}'
                sh 'docker push nikcladis/app'
                }
            }
        }
    }
}