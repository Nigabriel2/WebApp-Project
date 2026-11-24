
pipeline {
    agent any

    stages {
        stage('Install Dependencies') {
            steps {
                echo 'Installing Node.js dependencies...'
                sh 'npm ci'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running application tests...'
                sh 'npm test'
            }
        }

        stage('Deploy with Docker') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t coderwanda:latest .'

                echo 'Removing previous deployment if it exists...'
                sh 'docker rm -f coderwanda-deployment || true'

                echo 'Deploying application...'
                sh 'docker run -d --name coderwanda-deployment -p 3001:3000 coderwanda:latest'
            }
        }
    }

    post {
        success {
            echo 'Application deployed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}

