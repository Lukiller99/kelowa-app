pipeline {
    agent any
    environment {
        FIREBASE_DEPLOY_TOKEN = credentials('firebase-token')
    }
    stages {
        stage('Building') {
            steps {
                echo 'Building...'
                // Aquí podrías agregar pasos para instalar dependencias o compilar tu aplicación si es necesario
            }
        }
        stage('Testing Environment') {
            steps {
                sh 'firebase deploy -P devops-proj-testing --token "$FIREBASE_DEPLOY_TOKEN"'
                input message: 'After testing. Do you want to continue with Staging Environment? (Click "Proceed" to continue)'
            }
        }
        stage('Staging Environment') {
            steps {
                sh 'firebase deploy -P devops-proj-staging --token "$FIREBASE_DEPLOY_TOKEN"'
            }
        }
        stage('Production Environment') {
            steps {
                sh 'firebase deploy -P devops-proj-production-bcfd9 --token "$FIREBASE_DEPLOY_TOKEN"'
            }
        }
    }
}
