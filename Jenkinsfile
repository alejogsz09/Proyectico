pipeline {
    agent any

    environment {
        PROJECT_NAME = "Proyectico"
        VENV = ".venv"   // Nombre del entorno virtual
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Setup') {
            steps {
                sh '''
                    python3 -m venv ${VENV}
                    source ${VENV}/bin/activate
                    pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Lint') {
            steps {
                sh '''
                    source ${VENV}/bin/activate
                    pip install flake8
                    flake8 .
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                    source ${VENV}/bin/activate
                    pytest --maxfail=1 --disable-warnings -q
                '''
            }
        }

        stage('Package') {
            steps {
                sh '''
                    source ${VENV}/bin/activate
                    python setup.py sdist bdist_wheel || echo "No hay setup.py para empaquetar"
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
        always {
            echo "Pipeline finalizado."
        }
    }
}




