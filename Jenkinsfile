pipeline{
    agent any
    
    environment{
        ECR_REPO = 'node-app'
        FRONTEND_IMAGE = "${ECR_REPO}:frontend"
        BACKEND_IMAGE = "${ECR_REPO}:backend"
        CHATBACKEND_IMAGE = "${ECR_REPO}:chatbackend"
    }

    stages{
        stage('Fetch code'){
            steps{
                git branch:'develop', url: 'https://github.com/CharismaticOwl/Student_career_platform.git'
            }
        }
        stage('Containerize frontend'){
            sh 'docker build -t ${FRONTEND_IMAGE} frontend'
        }

        stage('Containerize backend'){
            sh 'docker build -t ${BACKEND_IMAGE} backend'
        }

        stage('Containerize chatbackend'){
            sh 'docker build -t ${CHATBACKEND_IMAGE} chatbackend'
        }

        stage('')
    }
}