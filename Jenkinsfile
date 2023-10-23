pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Install Requirements') {
            steps {
                bat 'python --version'
                bat 'pip install --user -r requirements.txt'
                bat 'pip install pytest'
            }
        }
        
        stage('Run Tests') {
            steps {
                bat 'python test_file.py'
            }
        }
    }
}
