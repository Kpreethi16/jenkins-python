pipeline {
    agent any

    environment {
        APP_NAME = 'python-jenkins-demo'
        VENV_DIR = 'venv'
        PYTHONPATH = '.'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Setup Virtual Environment') {
            steps {
                bat """
                    python --version
                    python -m venv %VENV_DIR%
                    call %VENV_DIR%\\Scripts\\activate
                    python -m pip install --upgrade pip
                    pip install -r requirements.txt
                """
            }
        }

        stage('Run Tests') {
            steps {
                bat """
                    call %VENV_DIR%\\Scripts\\activate
                    set PYTHONPATH=%PYTHONPATH%
                    pytest tests/
                """
            }
        }
    }

    post {
        success {
            echo 'Build and tests succeeded!'
        }
        failure {
            echo 'Build or tests failed.'
        }
    }
}
