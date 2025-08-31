pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM',
                    branches: [[name: 'main']],
                    userRemoteConfigs: [[url: 'https://github.com/losleandro/atividade-jenkins-devops.git']]
                ])
            }
        }

        stage('Cleanup') {
            steps {
                echo 'Parando e removendo containers antigos...'
                dir('atividade02/atividade02') {
                    sh 'docker-compose down -v || echo "Nada para remover"'
                }
            }
        }

        stage('Construção') {
            steps {
                echo 'Construindo containers...'
                dir('atividade02/atividade02') {
                    sh 'docker-compose build --no-cache'
                }
            }
        }

        stage('Entrega') {
            steps {
                echo 'Iniciando containers...'
                dir('atividade02/atividade02') {
                    sh 'docker-compose up -d'
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline concluído com sucesso!'
        }
        failure {
            echo 'Pipeline falhou. Verifique os logs.'
        }
    }
}
