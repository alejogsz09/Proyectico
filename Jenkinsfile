pipeline {
    agent any

    environment {
        PROJECT_NAME = "Proyectico"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install dependencies') {
            steps {
                sh '''
                    python3 -m pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                    pytest --maxfail=1 --disable-warnings -q
                '''
            }
        }
    }

    post {
        success {
            slackSend(
                channel: '#notificaciones_repo',
                message: "✅ Éxito: Job ${env.JOB_NAME} #${env.BUILD_NUMBER} en ${env.PROJECT_NAME}"
            )
        }
        failure {
            slackSend(
                channel: '#notificaciones_repo',
                message: "❌ Falló: Job ${env.JOB_NAME} #${env.BUILD_NUMBER} en ${env.PROJECT_NAME}"
            )
        }
    }
}





