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

        stage('Set up Python 3.10') {
            steps {
                script {
                    // Use a tool installer for Python 3.10
                    def pythonTool = tool name: 'Python 3.10', type: 'hudson.plugins.python.PythonInstallation'
                    def pythonHome = toolenv.PATH + "/${pythonTool}/bin"
                    env.PATH = "${pythonHome}:${env.PATH}"
                }
            }
        }

        stage('Install dependencies') {
            steps {
                script {
                    sh 'python -m pip install --upgrade pip'
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

    post {
        always {
            // Send email notification
            emailext (
                subject: "Test Results: ${currentBuild.result}",
                body: "The test results for the latest commit are: ${currentBuild.result}",
                recipientProviders: [[$class: 'DevelopersRecipientProvider']],
                to: 'i200471@nu.edu.pk',
                from: 'i201877@nu.edu.pk',
                replyTo: 'i201877@nu.edu.pk',
                smtpServer: 'smtp.example.com',
                smtpPort: '587',
                username: 'i201877@nu.edu.pk',
                password: env.MAIL_PASSWORD  // Set the MAIL_PASSWORD environment variable in Jenkins with the actual password
            )
        }
    }
}
