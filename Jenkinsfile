pipeline {
    agent any

    environment {
        DOCKER = 'C:\\Users\\Ishwarya\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe'
    }

    stages {
        stage('Docker Version') {
            steps {

                bat '"%DOCKER%" --version'
        }
    }

        stage('Build Docker Image') {
            steps {
                dir('ci-cd-pipeline-main'){
                bat '"%DOCKER%" build --no-cache -t vite-app .'
            }
        }
    }

        stage('Deploy Container') {
            steps {
                dir('ci-cd-pipeline-main'){
                bat '''
                "%DOCKER%" stop vite-container || echo Container not running
                "%DOCKER%" rm vite-container || echo Container not found
                "%DOCKER%" run -d -p 8081:80 --name vite-container vite-app
                '''
                }
            }
        }
    }
}