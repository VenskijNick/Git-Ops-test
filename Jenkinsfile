pipeline {
    agent any
    
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
                    // Сборка Docker-образа
                    def image = docker.build("192.168.64.19:5000/myapp:latest")
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    // Отправка Docker-образа в реестр
                    docker.withRegistry('http://192.168.64.19:5000') {
                        image.push()
                    }
                }
            }
        }
    }
}
