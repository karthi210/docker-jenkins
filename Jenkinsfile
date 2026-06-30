pipeline {
    agent any

    environment {
        IMAGE_NAME = "sample-app"
    }

    stages {

        stage('Clone') {
            steps {
                git branch: 'main', credentialsId: 'docker-01', url: 'https://github.com/karthi210/docker-jenkins.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop Existing Container') {
            steps {
                sh '''
                docker stop sample-container || true
                docker rm sample-container || true
                '''
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker run -d \
                --name sample-container \
                -p 3000:3000 \
                $IMAGE_NAME
                '''
            }
        }
    }
}
