pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Faz checkout direto na pasta "atividade02" para evitar confusão de diretórios
                checkout([$class: 'GitSCM',
                    branches: [[name: 'main']],
                    userRemoteConfigs: [[url: 'https://github.com/losleandro/atividade-jenkins-devops.git']],
                    extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'atividade02']]
                ])
            }
        }

        stage('Cleanup') {
            steps {
                echo 'Parando e removendo containers antigos...'
                dir('atividade02') {
                    sh 'docker-compose down -v || echo "Nada para remover"'
                }
            }
        }

        stage('Construção') {
            steps {
                echo 'Construindo containers...'
                dir('atividade02') {
                    sh 'docker-compose build --no-cache'
                }
            }
        }

        stage('Entrega') {
            steps {
                echo 'Subindo containers...'
                dir('atividade02') {
                    sh 'docker-compose up -d'
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline finalizado com sucesso!'
        }
        failure {
            echo 'Pipeline falhou. Verifique os logs.'
        }
    }
}
