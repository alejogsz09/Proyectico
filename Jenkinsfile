pipeline {
    agent any

    // --- CAMBIO PRINCIPAL AQUÍ ---
    // Jenkins buscará una herramienta Python configurada con este nombre.
    tools {
        python 'MiPython313'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Install dependencies') {
            steps {
                // No se necesita la ruta completa, Jenkins la agrega al PATH.
                bat 'python -m pip install --upgrade pip'
                bat 'python -m pip install -r requirements.txt'
            }
        }
        stage('Test') {
            steps {
                bat 'pytest'
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









