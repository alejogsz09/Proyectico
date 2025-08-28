pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Compilando..."
                // error intencional si quieres probar fallos
                // sh 'exit 1'
            }
        }
    }

    post {
        success {
            slackSend(channel: '#notificaciones-dev',
                      message: "✅ Éxito: Job ${env.JOB_NAME} #${env.BUILD_NUMBER}")
        }
        failure {
            slackSend(channel: '#notificaciones-dev',
                      message: "❌ Falló: Job ${env.JOB_NAME} #${env.BUILD_NUMBER}")
        }
        always {
            echo "Fin del pipeline"
        }
    }
}


