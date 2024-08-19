pipeline {
    agent any

    environment {
        REGISTRY_URL = "192.168.64.19:5000"  // URL вашего Docker Registry без протокола
        REGISTRY_CREDENTIALS_ID = "your-credentials-id"  // Идентификатор сохраненных учетных данных в Jenkins
        IMAGE_NAME = "myapp"  // Имя образа
        IMAGE_TAG = "latest"  // Тег образа
        DOCKER_IMAGE = "${REGISTRY_URL}/${IMAGE_NAME}:${IMAGE_TAG}"  // Полное имя образа
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
                script {
                    // Собираем Docker образ
                    docker.build("${DOCKER_IMAGE}")
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    // Логинимся в Docker Registry и пушим образ
                    docker.withRegistry("http://${REGISTRY_URL}", "${REGISTRY_CREDENTIALS_ID}") {
                        docker.image("${DOCKER_IMAGE}").push()
                    }
                }
            }
        }
    }
}
