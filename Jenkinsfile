pipeline {
    agent any

    triggers {
        githubPush()
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Downloading source code from GitHub'
                checkout scm
            }
        }

        stage('Compile') {
            steps {
                echo 'Compiling Python files'
               bat '"C:\\Users\\unars\\AppData\\Local\\Programs\\Python\\Python312\\python.exe" -m compileall -q .'
            }
        }

        stage('Test') {
            steps {
                echo 'Running Python unit tests'
                bat '"C:\\Users\\unars\\AppData\\Local\\Programs\\Python\\Python312\\python.exe" -m unittest -v'
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging Python application'
                bat 'powershell -NoProfile -Command "Compress-Archive -Path main.py,test_main.py,requirements.txt -DestinationPath python-app.zip -Force"'
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: 'python-app.zip'
            echo 'CI/CD Pipeline executed successfully!'
        }

        failure {
            echo 'CI/CD Pipeline failed!'
        }
    }
}