pipeline {
    agent any

    stages {

        stage('Install Dependencies') {
            steps {
                bat '''
                    py -3.14 -m venv venv

                    call venv\\Scripts\\activate.bat

                    python -m pip install --upgrade pip
                    python -m pip install -r requirements.txt
                    python -m pip install pytest pylint bandit
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
                body: "Build Successful\n${env.BUILD_URL}"
            )
        }

        failure {
            emailext(
                to: 'karankumar.vnbs@gmail.com',
                subject: "FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Build Failed\n${env.BUILD_URL}"
            )
        }

        always {
            cleanWs()
        }
    }
}