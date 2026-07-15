pipeline {
    agent any

    options {
        timestamps()
        disableConcurrentBuilds()
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Set Up') {
            steps {
                sh '''
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Verify') {
            steps {
                sh '''
                    . venv/bin/activate
                    python -m py_compile app.py
                    python -c "from app import app; print(app.url_map)"
                '''
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
    }
}