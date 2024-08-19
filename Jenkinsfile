pipeline {
    agent any

    environment {
        REGISTRY_URL = '192.168.64.19:5000'
        IMAGE_NAME = 'myapp:latest'
    }

    stages {
        stage('Checkout') {
            steps {
                // Получаем код из Git
                git 'https://github.com/VenskijNick/git-ops-test.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Сборка Docker-образа и сохранение его в переменную image
                    image = docker.build("${env.REGISTRY_URL}/${env.IMAGE_NAME}")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    // Отправка Docker-образа в реестр
                    docker.withRegistry("http://${env.REGISTRY_URL}") {
                        image.push()
                    }
                }
            }
        }
    }
}
