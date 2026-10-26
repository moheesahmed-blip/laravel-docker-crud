pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/<your-github-username>/laravel-docker-crud.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t <your-dockerhub-username>/laravel-app:latest .'
            }
        }
        stage('Push to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'dockerhub-token', variable: 'DOCKER_PASSWORD')]) {
                    sh 'echo $DOCKER_PASSWORD | docker login -u "<your-dockerhub-username>" --password-stdin'
                    sh 'docker push <your-dockerhub-username>/laravel-app:latest'
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
