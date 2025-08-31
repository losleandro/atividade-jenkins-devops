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
                script {
                    docker.build('atividade02', './atividade02')
                }
            }
        }

        stage('Entrega') {
            steps {
                echo 'Executando o container...'
                script {
                    docker.image('atividade02').run()
                }
            }
        }
    }
}
