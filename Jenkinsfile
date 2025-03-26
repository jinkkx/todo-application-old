
pipeline{
    agent any
    environment {
        DOCKER_HUB_CREDENTIALS = credentials('docker-hub-credentials')
    }
    stages{
        stage('Clone Repository'){
            steps{
                git branch: 'main', url: 'https://github.com/jinkkx/todo-application.git'
            }
        }

        stage('Build with Maven'){
            steps{
                sh 'mvn clean package -Dskiptests'
            }
        }

        stage('Build Docker Image'){
            steps{
                sh 'docker build -t todo-application-image:latest .'
            }
        }

        stage('Push Docker Image to Docker Hub'){
            steps{
                sh 'docker login -u jinkx -old -p Akola@123'
                sh 'docker tag todo-application-image:latest jinkxdocker/todo-application:latest'
                sh 'docker push jinkxdocker/todo-application:latest'
            }
        }

        stage('Verify Services'){
            steps{
                sh 'docker ps'
            }
        }

        stage('Clean Workplace'){
            steps{
                sh 'rm -rf *'
            }
        }
    }

    post {
        success {
            echo 'Build and Deployment Successful'
            }
            failure {
                echo 'Build and Deployment failure'
            }
    }
}
