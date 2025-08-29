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
                dir('atividade02') {
                    sh 'docker-compose down -v || true'
                }
            }
        }

        stage('Build') {
            steps {
                dir('atividade02') {
                    sh 'docker-compose build'
                }
            }
        }

        stage('Entrega') {
            steps {
                dir('atividade02') {
                    sh 'docker-compose up -d'
                }
            }
        }
    }

    post {
        always {
            echo "Pipeline finalizada"
        }
    }
}
