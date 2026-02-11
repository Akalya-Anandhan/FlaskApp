pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                echo 'Fetching Source Code...'
                checkout scm
            }
        }

        stage('Setup Python Environment') {
            steps {
                bat 'python -m venv venv'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat '.\\venv\\Scripts\\python -m pip install --upgrade pip'
                bat '.\\venv\\Scripts\\pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                bat '.\\venv\\Scripts\\pytest'
            }
        }

        stage('Deploy Flask App') {
            steps {
                echo 'Starting Flask App...'
                bat '.\\venv\\Scripts\\python app.py'
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline executed successfully!'
        }
        failure {
            echo '❌ Pipeline failed. Check logs.'
        }
    }
}
