pipeline {
    agent any  // El pipeline puede ejecutarse en cualquier agente disponible
    environment {
        // Aquí puedes definir variables globales si es necesario, por ejemplo:
        GITHUB_REPO = 'https://github.com/ehinar2112/pipeline.git'  // Repositorio de GitHub
        BRANCH = 'master'  // Rama que se utilizará (cámbiala si es necesario)
    }
    stages {
        // Etapa de "Checkout" para obtener el código del repositorio
        stage('Checkout') {
            steps {
                // Clonar el código desde GitHub usando las credenciales almacenadas
                git url: "${GITHUB_REPO}", branch: "${BRANCH}", credentialsId: 'github-credentials-id'
            }
        }
        // Etapa de "Install Dependencies" para instalar las dependencias necesarias
        stage('Install Dependencies') {
            steps {
                script {
                    // Si estás usando Composer (por ejemplo, en un proyecto PHP con WordPress)
                    // Instala dependencias con Composer
                    sh 'composer install'  // Si estás usando Composer para PHP
                    // Si usas npm para dependencias de frontend
                    // sh 'npm install'
                }
            }
        }

        // Etapa de "Run Tests" para ejecutar pruebas automatizadas
        stage('Run Tests') {
            steps {
                script {
                    // Ejecutar pruebas unitarias o de integración
                    // Ejemplo con PHPUnit para PHP:
                    sh 'vendor/bin/phpunit'  // Si usas PHPUnit
                    // Ejemplo con otro sistema de pruebas (si tienes pruebas de JavaScript, por ejemplo):
                    // sh 'npm test'   // Si usas Jest o Mocha para pruebas JS
                }
            }
        }
        // Etapa de "Build" si necesitas construir la aplicación antes de desplegarla
        stage('Build') {
            steps {
                script {
                    // Ejemplo de construcción (si usas Docker)
                    sh 'docker-compose build'  // Si usas Docker
                    // O cualquier otra construcción que necesites, como empaquetar archivos o crear contenedores
                }
            }
        }
        // Etapa de "Deploy" para desplegar tu proyecto
        stage('Deploy') {
            steps {
                script {
                    // Desplegar el proyecto, por ejemplo, usando Docker, FTP, o un servidor remoto
                    // Si estás usando Docker:
                    sh 'docker-compose up -d'  // Levantar el contenedor en segundo plano
                    // Si tu proyecto usa FTP o SSH para desplegar, podrías usar algo como:
                    // sh 'scp -r ./dist user@yourserver:/path/to/website'
                    // Si estás usando una herramienta como Ansible o AWS CLI para desplegar, ejecuta los comandos aquí.
                }
            }
        }
    }

    post {
        always {
            // Tareas que siempre se ejecutan al final del pipeline, independientemente del estado (éxito o fallo)
            echo 'El pipeline ha terminado.'
        }
        success {
            // Tareas que solo se ejecutan si el pipeline fue exitoso
            echo 'El pipeline se completó exitosamente.'
        }
        failure {
            // Tareas que solo se ejecutan si el pipeline falló
            echo 'El pipeline falló.'
        }
    }
}
