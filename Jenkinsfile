
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                bat 'docker build -t devops-store-image .'
            }
        }

        stage('Test') {
            steps {
                bat 'docker image inspect devops-store-image'
                bat 'if not exist index.html exit /b 1'
            }
        }

        stage('Deploy') {
            steps {
                bat 'docker rm -f devops-store 2>NUL || exit /b 0'
                bat 'docker run -d --name devops-store -p 8090:80 devops-store-image'
            }
        }
    }
}
