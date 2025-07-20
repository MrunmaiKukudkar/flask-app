pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker-hub-creds')
    }

    stages {
        stage('Clone Repository') {
            steps {
                git credentialsId: 'github-token', url: 'https://github.com/MrunmaiKukudkar/flask-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('mrunmaivilas/flask-app')
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub-creds') {
                        docker.image('mrunmaivilas/flask-app').push('latest')
                    }
                }
            }
        }
    }
}
