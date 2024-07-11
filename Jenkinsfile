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
                withCredentials([file(credentialsId: 'firebase-service-account', variable: 'FIREBASE_SERVICE_ACCOUNT_JSON')]) {
                    sh '''
                        export GOOGLE_APPLICATION_CREDENTIALS=$FIREBASE_SERVICE_ACCOUNT_JSON
                        firebase use --project kelowna-d0beb

                        firebase deploy --only hosting -P kelowna-d0beb-a1e56
                    '''
                }
                // input message: 'After testing. Do you want to continue with Staging Environment? (Click "Proceed" to continue)'
            }
        }
        stage('Staging Environment') {
            steps {
                withCredentials([file(credentialsId: 'firebase-service-account', variable: 'FIREBASE_SERVICE_ACCOUNT_JSON')]) {
                    sh '''
                        export GOOGLE_APPLICATION_CREDENTIALS=$FIREBASE_SERVICE_ACCOUNT_JSON
                        firebase use --project kelowna-d0beb

                        firebase deploy --only hosting -P kelowna-d0beb-a1e56
                    '''
                }
            }
        }
        stage('Production Environment') {
            steps {
                withCredentials([file(credentialsId: 'firebase-service-account', variable: 'FIREBASE_SERVICE_ACCOUNT_JSON')]) {
                    sh '''
                        export GOOGLE_APPLICATION_CREDENTIALS=$FIREBASE_SERVICE_ACCOUNT_JSON
                        firebase use --project kelowna-d0beb

                        firebase deploy --only hosting -P kelowna-d0beb-a1e56
                    '''
                }
            }
        }
    }
}
