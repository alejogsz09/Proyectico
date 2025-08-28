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
                    echo "📂 Estructura del workspace:"
                    ls -la

                    echo "🐍 Versiones instaladas:"
                    python3 --version
                    pip3 --version

                    if [ -f requirements.txt ]; then
                        echo "✅ requirements.txt encontrado, instalando dependencias..."
                        pip3 install --upgrade pip
                        pip3 install -r requirements.txt
                    else
                        echo "❌ ERROR: No se encontró requirements.txt en la raíz"
                        exit 1
                    fi
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                    echo "🚀 Ejecutando pruebas..."
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








