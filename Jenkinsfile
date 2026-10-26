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
                sh 'docker build -t mohees/laravel-app:latest .'
            }
        }
        stage('Push to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'dockerhub-token', variable: 'DOCKER_PASSWORD')]) {
                    sh 'echo $DOCKER_PASSWORD | docker login -u "mohees" --password-stdin'
                    sh 'docker push mohees/laravel-app:latest'
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s-deployment.yaml --validate=false'
            }
        }
    }
}