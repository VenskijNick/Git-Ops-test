pipeline {
    agent any

    environment {
        REGISTRY_URL = "http://192.168.64.19:5000"
        REGISTRY_CREDENTIALS_ID = "your-credentials-id"
        IMAGE_NAME = "myapp"
        IMAGE_TAG = "latest"
        DOCKER_IMAGE = "${REGISTRY_URL}/${IMAGE_NAME}:${IMAGE_TAG}"
    }

    stages {
        stage('Checkout') {
            steps {
                // Клонируем репозиторий
                git branch: 'master', url: 'https://github.com/VenskijNick/git-ops-test.git'
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
                // Логинимся в Docker Registry и пушим образ
                script {
                    docker.withRegistry("${REGISTRY_URL}", "${REGISTRY_CREDENTIALS_ID}") {
                        docker.image("${DOCKER_IMAGE}").push()
                    }
                }
            }
        }
    }
}
