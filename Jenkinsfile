pipeline {
    agent any

    stages {

        stage('Install Dependencies') {
            steps {
                bat '''
                    python -m venv venv

                    venv\\Scripts\\python.exe -m pip install --upgrade pip
                    venv\\Scripts\\python.exe -m pip install -r requirements.txt
                    venv\\Scripts\\python.exe -m pip install pytest pylint bandit
                '''
            }
        }

        stage('Lint') {
            steps {
                bat '''
                    venv\\Scripts\\pylint.exe app.py --exit-zero
                '''
            }
        }

        stage('Security Scan') {
            steps {
                bat '''
                    venv\\Scripts\\bandit.exe -r app.py -l || exit /b 0
                '''
            }
        }

        stage('Run Tests') {
            steps {
                bat '''
                    venv\\Scripts\\pytest.exe test_app.py -v --junitxml=report.xml
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
                    start "" /B venv\\Scripts\\python.exe app.py
                '''
            }
        }
    }

    post {

        success {
            emailext(
                to: 'karankumar.vnbs@gmail.com',
                subject: "SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """Build Successful

Job: ${env.JOB_NAME}
Build: ${env.BUILD_NUMBER}
URL: ${env.BUILD_URL}
"""
            )
        }

        failure {
            emailext(
                to: 'karankumar.vnbs@gmail.com',
                subject: "FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """Build Failed

Job: ${env.JOB_NAME}
Build: ${env.BUILD_NUMBER}
URL: ${env.BUILD_URL}
"""
            )
        }

        always {
            cleanWs()
        }
    }
}