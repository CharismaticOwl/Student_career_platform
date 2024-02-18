pipeline{
    agent any
    
    environment{
        ECR_REPO = '367065853931.dkr.ecr.ap-south-1.amazonaws.com/node-app'
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
            steps{
                script{
                    sh 'docker build -t ${FRONTEND_IMAGE} frontend'
                }
            }
        }

        stage('Containerize backend'){
            steps{
                script{
                    sh 'docker build -t ${BACKEND_IMAGE} backend'
                }
            }
        }

        stage('Containerize chatbackend'){
            steps{
                script{
                    sh 'docker build -t ${CHATBACKEND_IMAGE} chatbackend'
                }
            }
        }

        stage('Push images to AWS ECR'){
            steps{
                script{
                    withAWS(credentials: 'aws', region: 'ap-south-1') {
                        sh 'docker push ${FRONTEND_IMAGE}'
                        sh 'docker push ${FRONTEND_IMAGE}'
                        sh 'docker push ${FRONTEND_IMAGE}'
                    }
                }
            }
        }
    }
}