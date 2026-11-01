pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'GitHub code checked out by Jenkins'
            }
        }

        stage('Build') {
            steps {
                bat 'echo Building website...'
                bat 'if not exist dist mkdir dist'
                bat 'copy /Y index.html dist\\index.html'
            }
        }

        stage('Test') {
            steps {
                bat 'findstr /C:"Welcome to Jenkins" dist\\index.html'
            }
        }

        stage('Package') {
            steps {
                powershell 'Compress-Archive -Path dist -DestinationPath website.zip -Force'
                archiveArtifacts artifacts: 'website.zip', fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'GitHub Jenkins Pipeline SUCCESS!'
        }
        failure {
            echo 'Pipeline FAILED!'
        }
    }
}
