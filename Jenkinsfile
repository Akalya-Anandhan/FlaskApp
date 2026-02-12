pipeline {
    agent any

    environment {
        VENV_DIR = "venv"
    }

    stages {

        stage('Checkout Code') {
            steps {
                echo 'Cloning repository...'
                git branch: 'main', url: 'https://github.com/yourusername/FlaskApp.git'
            }
        }

        stage('Setup Environment') {
            steps {
                echo 'Creating virtual environment...'
                sh 'python3 -m venv venv'
                sh './venv/bin/pip install --upgrade pip'
                sh './venv/bin/pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                sh './venv/bin/python -m unittest discover -s tests'
            }
        }

        stage('Create Artifact') {
            steps {
                echo 'Creating ZIP artifact...'
                sh 'zip -r flask-app.zip .'
            }
        }
    }

   post {
    always {
        archiveArtifacts artifacts: 'flask-app.zip', fingerprint: true
        echo 'Pipeline finished!'
    }
    success {
        echo 'Build Successful!'
    }
    failure {
        echo 'Build Failed!'
    }
}

