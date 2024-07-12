pipeline {
    agent any
    stages {
        stage('Building') {
            steps {
                echo 'Building...'
                // Aquí podrías agregar pasos para instalar dependencias o compilar tu aplicación si es necesario
                // sh 'npm install'
                // sh 'npm run build'
            }
        }
        stage('Staging Environment') {
            when {
                not {
                    branch 'main'
                }

            }
            steps {
                withCredentials([file(credentialsId: 'firebase-service-account', variable: 'FIREBASE_SERVICE_ACCOUNT_JSON')]) {
                    sh '''
                        export GOOGLE_APPLICATION_CREDENTIALS=$FIREBASE_SERVICE_ACCOUNT_JSON
                        firebase use --project kelowna-d0beb

                        firebase target:clear hosting staging
                        firebase target:apply hosting staging kelowna-d0beb-a1e56
                        firebase deploy --only hosting:staging
                    '''
                }
            }
        }
        stage('Production Environment') {
            when {
                not{
                    branch 'main'
                }
            }
            steps {
                withCredentials([file(credentialsId: 'firebase-service-account', variable: 'FIREBASE_SERVICE_ACCOUNT_JSON')]) {
                    sh '''
                        export GOOGLE_APPLICATION_CREDENTIALS=$FIREBASE_SERVICE_ACCOUNT_JSON
                        firebase use --project kelowna-d0beb

                        firebase target:clear hosting production
                        firebase target:apply hosting production kelowna-d0beb-8dc23
                        firebase deploy --only hosting:production
                    '''
                }
            }
        }
    }
}
