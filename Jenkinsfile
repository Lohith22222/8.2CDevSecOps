pipeline {
    agent any

    options {
        skipDefaultCheckout(true)
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out nodejs-goof project from GitHub repository'
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing Node.js project dependencies using npm'
                bat 'call npm install'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running project tests. Pipeline continues even if tests fail.'
                bat 'call npm test || exit /b 0'
            }
        }

        stage('Generate Coverage Report') {
            steps {
                echo 'Generating coverage report if coverage script is available.'
                bat 'call npm run coverage || exit /b 0'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                echo 'Running npm audit to identify known dependency vulnerabilities.'
                bat 'call npm audit || exit /b 0'
            }
        }
    }
}
post {
    always {
        emailext (
            subject: "Build Result: ${currentBuild.currentResult}",
            body: "Job: ${env.JOB_NAME}\nBuild: ${env.BUILD_NUMBER}\nStatus: ${currentBuild.currentResult}",
            to: "lohith2823@gmail.com"
        )
    }
}
