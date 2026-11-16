
pipeline {
    agent any

    environment {
        DEPLOY_DIR = 'C:\\JenkinsDeploy'
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Downloading code from GitHub...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building Web Application...'
                bat 'dir'
                echo 'Build completed successfully!'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing Web Application...'
                bat '''
                if not exist index.html exit /b 1
                if not exist style.css exit /b 1
                if not exist script.js exit /b 1
                echo All required files are present!
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying Web Application...'
                bat '''
                if not exist "%DEPLOY_DIR%" mkdir "%DEPLOY_DIR%"
                copy /Y index.html "%DEPLOY_DIR%\\"
                copy /Y style.css "%DEPLOY_DIR%\\"
                copy /Y script.js "%DEPLOY_DIR%\\"
                '''
                echo 'Deployment completed!'
            }
        }
    }

    post {
        success {
            echo 'CI/CD Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed! Check Console Output.'
        }
    }
}
