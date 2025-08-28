pipeline {
    agent any

    stages {
        stage('Prueba Slack') {
            steps {
                echo "Ejecutando prueba de notificación en Slack..."
            }
        }
    }

    post {
        success {
            slackSend (
                channel: '#notificaciones-dev',
                color: 'good',
                message: "✅ Build exitoso en *${env.JOB_NAME}* #${env.BUILD_NUMBER} (<${env.BUILD_URL}|Ver detalles>)"
            )
        }
        failure {
            slackSend (
                channel: '#notificaciones-dev',
                color: 'danger',
                message: "❌ Falló el build en *${env.JOB_NAME}* #${env.BUILD_NUMBER} (<${env.BUILD_URL}|Ver detalles>)"
            )
        }
        always {
            slackSend (
                channel: '#notificaciones-dev',
                color: '#439FE0',
                message: "ℹ️ El pipeline finalizó (sea éxito o fallo) en *${env.JOB_NAME}* #${env.BUILD_NUMBER}"
            )
        }
    }
}

