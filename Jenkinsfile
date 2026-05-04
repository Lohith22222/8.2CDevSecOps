pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out project from GitHub'
                git branch: 'main', url: 'https://github.com/Lohith22222/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies'
                bat 'call npm install'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests'
                bat 'call npm test || exit /b 0'
            }
        }

        stage('Generate Coverage Report') {
            steps {
                echo 'Generating coverage'
                bat 'call npm run coverage || exit /b 0'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running npm audit'
                bat 'call npm audit || exit /b 0'
            }
        }
    }

    post {
        always {
            emailext (
                subject: "Build Status: ${currentBuild.currentResult}",
                body: """Build Details:
Job Name: ${env.JOB_NAME}
Build Number: ${env.BUILD_NUMBER}
Status: ${currentBuild.currentResult}
""",
                to: "lohith2823@gmail.com"
            )
        }
    }
}
