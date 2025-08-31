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
                // Usando shell para construir a imagem
                sh 'docker build -t atividade02 ./atividade02'
            }
        }

        stage('Entrega') {
            steps {
                echo 'Executando o container...'
                // Usando shell para rodar o container
                sh 'docker run --rm atividade02'
            }
        }
    }
}
