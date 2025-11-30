pipeline {
    agent {
        docker {
            image 'mohamedhelmy/android-docker:34'   // Android SDK + build-tools + platform-tools
            args '--user root'
        }
    }

    tools {
        gradle 'gradle-8'     // имя gradle tool в Jenkins -> Manage Jenkins -> Global Tool Configuration
        jdk 'jdk17'           // JDK из Jenkins
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Debug') {
            steps {
                sh 'gradle assembleDebug'
            }
        }

        stage('Unit Tests') {
            steps {
                sh 'gradle test'
            }
        }

        stage('Optional Release Build') {
            when {
                branch 'main'
            }
            steps {
                sh 'gradle assembleRelease'
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: '**/build/outputs/**/*.apk', fingerprint: true
            junit '**/build/test-results/**/*.xml'
        }
    }
}
