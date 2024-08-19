pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "yourdockerhubusername/yourimagename:${env.BUILD_ID}"
    }

    stages {
        stage('Checkout') {
            steps {
                // Клонируем репозиторий
                git branch: 'master', url: 'https://github.com/your-repository-url.git'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                // Собираем Docker образ
                script {
                    docker.build("${DOCKER_IMAGE}")
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                // Логинимся в DockerHub и пушим образ
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                        docker.image("${DOCKER_IMAGE}").push()
                    }
                }
            }
        }
    }
}
