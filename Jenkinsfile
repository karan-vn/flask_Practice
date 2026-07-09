pipeline {
    agent any

    environment {
        PYTHONPATH = "${WORKSPACE}"
        PATH = "C:\\Users\\Admin\\AppData\\Local\\Programs\\Python\\Python314;C:\\Users\\Admin\\AppData\\Local\\Programs\\Python\\Python314\\Scripts;${env.PATH}"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                bat '''
                    python -m venv venv
                    call venv\\Scripts\\activate.bat

                    python -m pip install --upgrade pip
                    pip install -r requirements.txt

                    pip install pytest
                    pip install pylint
                    pip install bandit
                '''
            }
        }

        stage('Lint') {
            steps {
                bat '''
                    call venv\\Scripts\\activate.bat
                    pylint app.py --exit-zero
                '''
            }
        }

        stage('Security Scan') {
            steps {
                bat '''
                    call venv\\Scripts\\activate.bat
                    bandit -r app.py -l
                '''
            }
        }

        stage('Run Tests') {
            steps {
                bat '''
                    call venv\\Scripts\\activate.bat
                    pytest test_app.py -v --junitxml=report.xml
                '''
            }

            post {
                always {
                    junit 'report.xml'
                }
            }
        }

        stage('Deploy') {
            steps {
                bat '''
                    taskkill /F /IM python.exe 2>nul || ver>nul
                    start /B venv\\Scripts\\python.exe app.py
                    echo Application deployed successfully on port 5000.
                '''
            }
        }
    }

    post {

        success {
            emailext(
                to: 'karankumar.vnbs@gmail.com',
                subject: "SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
Pipeline completed successfully.

Job Name: ${env.JOB_NAME}
Build Number: ${env.BUILD_NUMBER}
Build URL: ${env.BUILD_URL}
"""
            )
        }

        failure {
            emailext(
                to: 'karankumar.vnbs@gmail.com',
                subject: "FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
Pipeline failed.

Job Name: ${env.JOB_NAME}
Build Number: ${env.BUILD_NUMBER}
Build URL: ${env.BUILD_URL}
"""
            )
        }

        always {
            cleanWs()
        }
    }
}