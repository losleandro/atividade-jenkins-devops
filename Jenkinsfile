pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Faz o clone direto no workspace
                git branch: 'main',
                    url: 'https://github.com/losleandro/atividade-jenkins-devops.git'
            }
        }

        stage('Cleanup') {
            steps {
                // Para qualquer container anterior e remove volumes
                sh 'docker-compose down -v || true'
            }
        }

        stage('Build') {
            steps {
                // Constrói as imagens definidas no docker-compose.yml
                sh 'docker-compose build'
            }
        }

        stage('Entrega') {
            steps {
                // Sobe os containers em background
                sh 'docker-compose up -d'
            }
        }
    }

    post {
        always {
            echo "Pipeline finalizada"
        }
    }
}
