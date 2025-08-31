pipeline {
    agent any

    environment {
        COMPOSE_PROJECT_NAME = 'atividade02'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: 'main']],
                    userRemoteConfigs: [[
                        url: 'https://github.com/losleandro/atividade-jenkins-devops.git'
                    ]]
                ])
            }
        }

        stage('Cleanup') {
            steps {
                dir('atividade02') {
                    echo 'Parando e removendo containers antigos...'
                    bat 'docker-compose down -v'
                }
            }
        }

        stage('Build') {
            steps {
                dir('atividade02') {
                    echo 'Buildando containers...'
                    bat 'docker-compose build --no-cache'
                }
            }
        }

        stage('Up') {
            steps {
                dir('atividade02') {
                    echo 'Subindo containers...'
                    bat 'docker-compose up -d'
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline finalizada com sucesso!'
        }
        failure {
            echo 'Pipeline falhou. Verifique os logs.'
        }
    }
}
