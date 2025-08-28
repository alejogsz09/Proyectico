pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Compilando..."
                // fuerza un fallo para probar la notificación
                sh 'exit 1'
            }
        }
    }

    post {
        success {
            slackSend(channel: '#notificaciones_repo',
                      message: "✅ Éxito: Job ${env.JOB_NAME} #${env.BUILD_NUMBER}")
        }
        failure {
            slackSend(channel: '#notificaciones_repo',
                      message: "❌ Falló: Job ${env.JOB_NAME} #${env.BUILD_NUMBER}")
        }
        always {
            echo "Fin del pipeline"
        }
    }
}



