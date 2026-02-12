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
                bat 'python -m venv venv'
                bat 'venv\\Scripts\\pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                bat 'venv\\Scripts\\python -m unittest discover -s tests'
            }
        }

        stage('Create Artifact') {
            steps {
                echo 'Creating ZIP file...'
                bat 'powershell Compress-Archive -Path * -DestinationPath flask-app.zip -Force'
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

