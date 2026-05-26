pipeline {

    agent any

    stages {

        stage('Clone') {
            steps {
                git 'https://github.com/kapilkhurana89/python-cicd-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t python-app:v1 .'
            }
        }

        stage('Load Image to Minikube') {
            steps {
                bat 'minikube image load python-app:v1'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat 'kubectl apply -f k8s/deployment.yaml'
                bat 'kubectl apply -f k8s/service.yaml'
            }
        }
    }
}