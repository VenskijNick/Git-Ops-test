pipeline {
    agent any

    environment {
        REGISTRY_URL = "192.168.64.19:5000"  // URL вашего Docker Registry без протокола
        REGISTRY_CREDENTIALS_ID = "a2a0be2f-8d7a-4005-a7e6-8d36f669323c"  // Идентификатор сохраненных учетных данных в Jenkins
        IMAGE_NAME = "myapp"  // Имя образа
        IMAGE_TAG = "latest"  // Тег образа
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
                    // Формируем полное имя Docker-образа
                    def dockerImage = "${REGISTRY_URL}/${IMAGE_NAME}:${IMAGE_TAG}"

                    // Собираем Docker образ
                    docker.build(dockerImage)
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    // Логинимся в Docker Registry и пушим образ
                    def dockerImage = "${REGISTRY_URL}/${IMAGE_NAME}:${IMAGE_TAG}"
                    docker.withRegistry("http://${REGISTRY_URL}", "${REGISTRY_CREDENTIALS_ID}") {
                        docker.image(dockerImage).push()
                    }
                }
            }
        }
    }
}
