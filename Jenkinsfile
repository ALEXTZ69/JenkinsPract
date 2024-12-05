pipeline {
    agent any

    tools {
        nodejs "Node18" // Configura una instalación de Node.js en Jenkins
    }

    stages {
        stage('Debug Info') {
            steps {
                sh '''
                    echo "Verificando ubicación actual:"
                    pwd
                    echo "\nListando archivos:"
                    ls -la
                    echo "\nVerificando Docker:"
                    which docker || echo "Docker no encontrado"
                '''
            }
        }
        stage('Construir Imagen Docker') {
            steps {
                sh '''
                    echo "Intentando construir imagen..."
                    docker build -t hola-mundo-node:latest . || echo "Error al construir"
                '''
            }
        }

        stage('Ejecutar Contenedor Node.js') {
            steps {
                sh '''
                    echo "Intentando ejecutar contenedor..."
                    docker stop hola-mundo-node || true
                    docker rm hola-mundo-node || true
                    docker run -d --name hola-mundo-node -p 3000:3000 hola-mundo-node:latest
                '''
            }
        }
    }
}