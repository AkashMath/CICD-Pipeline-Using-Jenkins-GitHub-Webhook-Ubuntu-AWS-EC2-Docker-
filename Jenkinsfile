pipeline {
    agent any 

    environment {
        // Define any environment variables here
    CONTAINER_NAME = 'nestjs-app'
    IMAGE_NAME = 'nesths-image'
    EMAIL = 'akashmathpal6@gmail.com' 
    PORT = '3000'
    }

    stages {
        stages ('Clone Repository') {
            steps {
                git branch: 'main', url: "https://github.com/AkashMath/CICD-Pipeline-Using-Jenkins-GitHub-Webhook-Ubuntu-AWS-EC2-Docker-.git"
            }
        } 
        stage ('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t $IMAGE_NAME ."
                }
            }
        } 

          stage ('Stop & Remove Existing Container') {
            steps {
           '''
           docker stop ${CONTAINER_NAME} || true
           docker rm ${CONTAINER_NAME} || true
           '''
            }
        }
          stage ('Docker Container Run') {
            steps {
             '''
             docker run -d -p ${PORT}:${PORT} 
             --name $CONTAINER_NAME $IMAGE_NAME
             '''
            }
        }  
        stage ('send email notification') {
            steps {
                emailext(
                    subject: "Nestjs App Deployed Successfully on EC2",
                    body: "The Nestjs application has been successfully deployed on the EC2 instance. 
                    You can access it at http://<EC2_PUBLIC_IP>:
                    http://65.0.76.10:8080:${PORT}/",
                    to: "${EMAIL}"
                )
            }
        }    
     }
}