pipeline {
    agent any

    stages {
        // stage('Checkout') {
        //     steps {
        //         // Clona tu repositorio o realiza cualquier acción necesaria para obtener el código fuente
        //         git 'https://github.com/tu-usuario/tu-repo.git'
        //     }
        // }

        stage('Build') {
            steps {
                // No se necesita ninguna acción de compilación explícita para archivos estáticos
            }
        }

        stage('Deploy to Firebase Hosting') {
            steps {
                // Utiliza Firebase CLI para desplegar a Firebase Hosting
                script {
                    def FIREBASE_TOKEN = credentials('firebase-service-account')

                    // Instalar Firebase CLI si no está instalado
                    sh 'npm install -g firebase-tools'

                    // Autenticar con Firebase usando el archivo de cuenta de servicio
                    withCredentials([file(credentialsId: 'firebase-service-account', variable: 'FIREBASE_SERVICE_ACCOUNT')]) {
                        sh 'firebase use --token "$FIREBASE_SERVICE_ACCOUNT"'
                        sh 'firebase deploy --only hosting'
                    }
                }
            }
        }
    }
}
