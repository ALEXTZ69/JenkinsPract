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
                    echo "Deteniendo contenedor anterior si existe..."
                    docker ps -a | grep hola-mundo-node || echo "No hay contenedor previo"
                    docker stop hola-mundo-node || echo "No se pudo detener el contenedor"
                    docker rm hola-mundo-node || echo "No se pudo eliminar el contenedor"
                    
                    echo "Ejecutando nuevo contenedor..."
                    docker run -d --name hola-mundo-node -p 3000:3000 hola-mundo-node:latest
                    
                    echo "Verificando estado del contenedor:"
                    docker ps | grep hola-mundo-node || echo "Contenedor no está corriendo"
                    docker logs hola-mundo-node
                '''
            }
        }
    }
}