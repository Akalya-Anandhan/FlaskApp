pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                echo 'Cloning repository...'
                git branch: 'main', url: 'https://github.com/Akalya-Anandhan/FlaskApp.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies...'
                sh 'python3 -m venv venv'
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
                echo 'Creating ZIP file...'
                sh 'zip -r flask-app.zip .'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'flask-app.zip', fingerprint: true
            echo 'Pipeline finished'
        }
    }
}


