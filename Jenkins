pipeline {
    agent any

    stages {
        stage('Cleanup') {
            steps {
                echo 'Limpando workspace...'
                deleteDir()  // limpa arquivos antigos
            }
        }

        stage('Checkout') {
            steps {
                echo 'Clonando repositório...'
                git url: 'https://github.com/losleandro/atividade-jenkins-devops.git'
            }
        }

        stage('Construção') {
            steps {
                echo 'Instalando dependências e construindo app...'
                sh 'python -m venv venv'
                sh 'venv/bin/pip install --upgrade pip'
                sh 'venv/bin/pip install -r requirements.txt'
            }
        }

        stage('Entrega') {
            steps {
                echo 'Rodando aplicação...'
                sh 'venv/bin/python main.py &'
            }
        }
    }
}
