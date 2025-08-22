pipeline {
    agent any

    environment {
        CONTAINER_NAME = "nestjs-app"
        IMAGE_NAME = "nesths-image"
        EMAIL = "akashmathpal6@gmail.com"
        PORT = "3000"
    }

    stages {
        stage('Clone Repo'){
            steps{
                git branch: 'main', url: 'https://github.com/AkashMath/CICD-Pipeline-Using-Jenkins-GitHub-Webhook-Ubuntu-AWS-EC2-Docker-.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }
        stage('Stop & Remove Previous Container') {
            steps {
                sh '''
                    docker stop $CONTAINER_NAME || true
                    docker rm $CONTAINER_NAME || true
                '''
            }
        }
        stage('Docker Container Run') {
            steps {
                sh '''
                    docker run -d -p ${PORT}:${PORT} --name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }
        stage('Send Email Notification') {
            steps {
               emailext(
                subject: "NestJS App Deployed Successfully on EC2!",
                body: "Your Nest JS app is Deployed! http://13.232.169.228:${PORT}/",
                to: "${EMAIL}"
               )
            }
        }

    }
}
