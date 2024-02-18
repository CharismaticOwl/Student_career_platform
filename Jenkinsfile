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
                    
                    frontendImage = docker.build("${FRONTEND_IMAGE}","frontend")
                }
            }
        }

        stage('Containerize backend'){
            steps{
                script{
                    
                    backendendImage = docker.build("${BACKEND_IMAGE}","backend")
                }
            }
        }

        stage('Containerize chatbackend'){
            steps{
                script{
                    
                    chatbackendImage = docker.build("${CHATBACKEND_IMAGE}","chatbackend")
                }
            }
        }
        

        stage('Push images to AWS ECR'){
            steps{
                script{
                    docker.withRegistry('https://367065853931.dkr.ecr.ap-south-1.amazonaws.com', 'ecr:ap-south-1:aws') {
                    frontendImage.push()
                    backendendImage.push()
                    chatbackendImage.push()
                }
            }
        }
    }
}
}