pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/TU_USUARIO/ejemplo-jenkins-slack.git'
            }
        }

        stage('Instalar dependencias') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Tests') {
            steps {
                sh 'pytest tests/ --maxfail=1 --disable-warnings -q'
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
    }
}
