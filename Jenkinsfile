pipeline {
    agent any

    stages {
        stage('Cleanup') {
            steps {
                echo 'Limpando workspace...'
                deleteDir()
            }
        }

        stage('Checkout') {
            steps {
                echo 'Fazendo checkout do código...'
                git branch: 'main', url: 'https://github.com/losleandro/atividade-jenkins-devops.git'
            }
        }

        stage('Construção') {
            steps {
                echo 'Construindo a imagem Docker...'
                // Usando shell em vez da API Docker do Jenkins
                sh 'docker build -t ./atividade02'
            }
        }

        stage('Entrega') {
            steps {
                echo 'Executando container...'
                sh 'docker run --rm atividade02'
            }
        }
    }
}
