pipeline {
    agent any
    environment {
        DOCKER_HUB_CREDENTIALS = credentials('docker-hub-credentials')
    }
    stages{
        stage('Clone Repository'){
            steps{
                git branch: 'master', url: 'https://github.com/PankhudiJain17/todo-application.git'
            }
        }
        stage('builds with maven'){
            steps{
                sh 'mvn clean package -Dskiptests'
            }
        }
        stage('Build Docker Image'){
            steps{
                sh 'docker build -t todo-application-image:latest .'
            }
        }
        stage('push image to docker hub'){
            steps{
                sh 'docker login -u <username> -p <password>'
                sh 'docker tag todo-application-image:latest <username>/todo-application-image:latest'
                sh 'docker push <username>/todo-application-image:latest'
            }
        }
        stage('Verify services'){
            steps{
                sh 'docker ps'
            }
        }
        stage('Clean Workspace'){
            steps{
                sh 'rm -rf *'
            }
        }
    }
    post{
        success {
            echo 'Build and deployment successful'
        }
        failure{
            echo 'Build and Deployment Failed'
        }
    }
}
