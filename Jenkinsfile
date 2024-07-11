pipeline {
    agent any
    stages {
        stage('Staging Environment') {
            steps {
                withCredentials([file(credentialsId: 'firebase-service-account', variable: 'FIREBASE_SERVICE_ACCOUNT_JSON')]) {
                    sh '''
                        export GOOGLE_APPLICATION_CREDENTIALS=$FIREBASE_SERVICE_ACCOUNT_JSON
                        firebase use --project kelowna-d0beb
                        firebase deploy --only hosting -P staging
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
                        firebase deploy --only hosting -P production
                    '''
                }
            }
        }
    }
}
