pipeline {

    agent any

    tools {
        git 'Git'
    }

    environment {
        IMAGE_NAME = "python-app"
        IMAGE_TAG  = "v1"
    }

    stages {

        stage('Clone Code') {
            steps {
                git branch: 'main',
                url: 'https://github.com/kapilkhurana89/python-cicd-project.git'
            }
        }

        stage('Check Docker Version') {
            steps {
                bat 'docker --version'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat "docker build -t %IMAGE_NAME%:%IMAGE_TAG% ."
            }
        }

        stage('Check Docker Images') {
            steps {
                bat 'docker images'
            }
        }

        stage('Load Image to Minikube') {
            steps {
                bat "minikube image load %IMAGE_NAME%:%IMAGE_TAG%"
            }
        }

        stage('Verify Image in Minikube') {
            steps {
                bat 'minikube ssh "docker images"'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat 'kubectl apply -f k8s/deployment.yaml'
                bat 'kubectl apply -f k8s/service.yaml'
            }
        }

        stage('Verify Kubernetes Resources') {
            steps {
                bat 'kubectl get pods'
                bat 'kubectl get svc'
                bat 'kubectl get deployments'
            }
        }
    }

    post {

        success {
            echo 'Pipeline executed successfully!'
        }

        failure {
            echo 'Pipeline failed!'
        }
    }
}