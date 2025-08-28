pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Install dependencies') {
            steps {
                bat 'python -m pip install --upgrade pip'
                bat 'python -m pip install -r requirements.txt'
            }
        }
        stage('Test') {
            steps {
                bat 'pytest || exit 1'
            }
        }
    }

    post {
        success {
            slackSend(channel: '#notificaciones_repo', message: "✅ Build passed en ${env.JOB_NAME} #${env.BUILD_NUMBER}")
        }
        failure {
            slackSend(channel: '#notificaciones_repo', message: "❌ Build failed en ${env.JOB_NAME} #${env.BUILD_NUMBER}")
        }
    }
}









