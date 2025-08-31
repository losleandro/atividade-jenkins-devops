pipeline {
    agent any

    environment {
        APP_DIR = "."   // trabalhar na raiz do repositório
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Fazendo checkout do repositório..."
                checkout([$class: 'GitSCM',
                    branches: [[name: 'main']],
                    userRemoteConfigs: [[url: 'https://github.com/losleandro/atividade-jenkins-devops.git']]
                ])
            }
        }

        stage('Cleanup') {
            steps {
                echo "Limpando containers e imagens antigas..."
                dir("${APP_DIR}") {
                    sh 'docker-compose down --rmi all -v || true'
                }
            }
        }

        stage('Construção') {
            steps {
                echo "Construindo containers..."
                dir("${APP_DIR}") {
                    sh 'docker-compose build --no-cache'
                }
            }
        }

        stage('Entrega') {
            steps {
                echo "Subindo containers..."
                dir("${APP_DIR}") {
                    sh 'docker-compose up -d'
                }
            }
        }
    }

    post {
        success { echo 'Pipeline finalizada com sucesso!' }
        failure { echo 'Pipeline falhou!' }
    }
}
