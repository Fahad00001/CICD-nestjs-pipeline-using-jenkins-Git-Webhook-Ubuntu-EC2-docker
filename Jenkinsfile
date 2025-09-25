pipeline {
    agent any   

    environment {
        CONTAINER_NAME = 'nestjs-app1'
        IMAGE_NAME = 'nestjs-image'
        EMAIL_RECIPIENT = 'fahad.iq010@gmial.com'
        PORT = '3000'
    }

    stages {
        stage('Clone repo') {
            steps {
                git branch: 'main', url: 'https://github.com/Fahad00001/CICD-nestjs-pipeline-using-jenkins-Git-Webhook-Ubuntu-EC2-docker.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop and Remove Previous Container') {
            steps {
                sh '''
                     docker stop $CONTAINER_NAME || true
                     docker rm $CONTAINER_NAME || true
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                     docker run -d -p ${PORT}:${PORT} --name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }

        stage('Send Email Notification') {
            steps {
                emailext(
                    subject: "NestJS app deployed successfully on EC2",
                    body: "The NestJS application has been successfully deployed and is running on port http://13.210.204.71:${PORT}.",
                    to: "${EMAIL_RECIPIENT}"
                )
            }
        }
    }   
}
