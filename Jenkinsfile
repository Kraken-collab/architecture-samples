pipeline {
    agent any

    
    tools {
        gradle 'gradle-8'  
        jdk 'jdk17'
    }
    
    stage('Setup local.properties') {
        steps {
            writeFile file: 'local.properties', text: "sdk.dir=/opt/android-sdk\n"
        }
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

        stage('Run Tests') {
            steps {
                sh 'gradle test'
            }
        }

        stage('Archive APK') {
            steps {
                archiveArtifacts artifacts: '**/build/outputs/**/*.apk'
            }
        }
    }
}
