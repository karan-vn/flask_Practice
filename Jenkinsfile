pipeline {
    agent any

    stages {
        stage('Check Python') {
            steps {
                bat '''
                    where py
                    py --version
                    py -0p
                '''
            }
        }
    }
}