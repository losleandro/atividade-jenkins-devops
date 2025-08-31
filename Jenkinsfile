pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Cleanup') {
            steps {
                echo 'Parando e removendo containers antigos...'
                sh 'docker-compose down -v || echo "Nada para remover"'
            }
        }

        stage('Construção') {
            steps {
                echo 'Construindo containers...'
                sh 'docker-compose build --no-cache'
            }
        }

        stage('Entrega') {
            steps {
                echo 'Iniciando containers...'
                sh 'docker-compose up -d'
            }
        }
    }

    post {
        failure {
            echo 'Pipeline falhou. Verifique os logs.'
        }
    }
}
