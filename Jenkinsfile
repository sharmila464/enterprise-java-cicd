pipeline {
    agent any
    environment {
        DOCKER_HUB_CREDENTIALS = credentials('docker-hub-creds-id')
        IMAGE_NAME = 'sharmila9892/demo-app'
    }
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/sharmila464/enterprise-java-cicd.git', branch: 'main'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Docker Build & Push') {
            steps {
                script {
                    dockerImage = docker.build("${IMAGE_NAME}:latest")
                    docker.withRegistry('', DOCKER_HUB_CREDENTIALS) {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}

