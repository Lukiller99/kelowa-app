pipeline {
    agent any
    stages {
        stage('Building') {
            steps {
                echo 'Building...'
                // Aquí podrías agregar pasos para instalar dependencias o compilar tu aplicación si es necesario
            }
        }
        stage('Testing Environment') {
            steps {
                withCredentials([file(credentialsId: 'firebase-service-account', variable: 'FIREBASE_SERVICE_ACCOUNT')]) {
                    sh 'firebase use --token "$FIREBASE_SERVICE_ACCOUNT"'
                    sh 'firebase deploy -P devops-proj-testing --token "$FIREBASE_SERVICE_ACCOUNT"'
                }
                input message: 'After testing. Do you want to continue with Staging Environment? (Click "Proceed" to continue)'
            }
        }
        stage('Staging Environment') {
            steps {
                withCredentials([file(credentialsId: 'firebase-service-account', variable: 'FIREBASE_SERVICE_ACCOUNT')]) {
                    sh 'firebase use --token "$FIREBASE_SERVICE_ACCOUNT"'
                    sh 'firebase deploy -P devops-proj-staging --token "$FIREBASE_SERVICE_ACCOUNT"'
                }
            }
        }
        stage('Production Environment') {
            steps {
                withCredentials([file(credentialsId: 'firebase-service-account', variable: 'FIREBASE_SERVICE_ACCOUNT')]) {
                    sh 'firebase use --token "$FIREBASE_SERVICE_ACCOUNT"'
                    sh 'firebase deploy -P devops-proj-production-bcfd9 --token "$FIREBASE_SERVICE_ACCOUNT"'
                }
            }
        }
    }
}
