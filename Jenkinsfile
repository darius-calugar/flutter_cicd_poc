pipeline {
    agent any
    stages {
        stage ('Get Dependencies') {
            steps {
                sh "flutter pub get"
            }
        }
        stage ('Flutter Analysis') {
            steps {
                sh "dart analyze . --fatal-infos"
            }
        }
        stage ('Flutter Build APK') {
            steps {
                script {
                    if (env.BRANCH_NAME == 'master') {
                        sh "flutter build apk --split-per-abi --dart-define=ENV=prod"
                    } else {
                        sh "flutter build apk --split-per-abi --dart-define=ENV=dev"
                    }
                }
            }
        }
        stage('Flutter Build iOS') {
            steps {
                script {
                    if (env.BRANCH_NAME == 'master') {
                        sh "flutter build ios --release --no-codesign --dart-define=ENV=prod"
                    } else {
                        sh "flutter build ios --release --no-codesign --dart-define=ENV=dev"
                    }
                }
            }
        }
        stage('Cleanup') {
            steps {
                sh "flutter clean"
            }
        }
    }
}