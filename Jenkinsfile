pipeline {
    agent any

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
                echo 'Parando e removendo containers antigos...'
                bat 'docker-compose down -v'
            }
        }

        stage('Build') {
            steps {
                echo 'Buildando containers...'
                bat 'docker-compose build --no-cache'
            }
        }

        stage('Up') {
            steps {
                echo 'Subindo containers...'
                bat 'docker-compose up -d'
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
