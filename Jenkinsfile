pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checkout stage started'
                bat 'git --version'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the application'
                bat 'if exist index.html (echo Build successful) else (exit /b 1)'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing the application'
                bat 'findstr /C:"Welcome to CI/CD Pipeline" index.html'
                bat 'findstr /C:"Application Successfully Deployed!" index.html'
                echo 'All tests passed'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application'
                bat 'if not exist deployed-site mkdir deployed-site'
                bat 'copy /Y index.html deployed-site\\index.html'
                archiveArtifacts artifacts: 'deployed-site/index.html', fingerprint: true
                echo 'Application deployed successfully'
            }
        }
    }

    post {
        success {
            echo 'CI/CD PIPELINE COMPLETED SUCCESSFULLY!'
        }
        failure {
            echo 'Pipeline failed. Check Console Output.'
        }
    }
}