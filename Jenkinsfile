pipeline {
    agent any

    stages {
        stage('Checkout code') {
            steps {
                script {
                    checkout scm
                }
            }
        }


        stage('Install dependencies') {
            steps {
                script {
                    sh 'pip install -r requirements.txt'
                    sh 'pip install pytest'
                }
            }
        }

        stage('Test with pytest') {
            steps {
                script {
                    sh 'python3 test_file.py'
                }
            }
        }
    }

}
