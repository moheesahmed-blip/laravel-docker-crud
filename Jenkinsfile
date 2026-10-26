pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/moheesahmed-blip/laravel-docker-crud.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t moheesahmed-blip/laravel-app:latest .'
            }
        }
        stage('Push to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'dockerhub-token', variable: 'DOCKER_PASSWORD')]) {
                    sh 'echo $DOCKER_PASSWORD | docker login -u "moheesahmed-blip" --password-stdin'
                    sh 'docker push moheesahmed-blip/laravel-app:latest'
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s-deployment.yaml'
            }
        }
    }
}