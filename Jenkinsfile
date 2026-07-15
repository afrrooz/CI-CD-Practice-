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
                sh 'python3 -m pip install --upgrade pip'
                sh 'python3 -m pip install -r requirements.txt'
            }
        }

        stage('Verify') {
            steps {
                sh 'python3 -m py_compile app.py'
                sh 'python3 -c "from app import app; print(app.url_map)"'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
    }
}