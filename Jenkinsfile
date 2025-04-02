pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'rayan94z/spring-app'
        DOCKER_CREDENTIALS = 'docker-hub'
    }

    tools {
        jdk 'JDK-17'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/RayanA94/Jenkins'
            }
        }

        stage('Build Application') {
            steps {
                sh './gradlew clean build -x test'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}:latest")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDENTIALS) {
                        docker.image("${DOCKER_IMAGE}:latest").push()
                    }
                }
            }
        }
    }
}
