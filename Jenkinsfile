pipeline {
    agent any

    environment {
        GRADLE_HOME = tool 'Gradle' // Assumes Gradle is configured in Jenkins global tools
        JAVA_HOME = tool 'JDK11'   // Assumes JDK 11 is configured in Jenkins global tools
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                script {
                    // Use Gradle Wrapper to build the project
                    sh 'gradle init'
                    sh 'gradle build'
                }
            }
        }
       stage('Install Android SDK') {
            steps {
                script {
                    sh '''
                        wget https://dl.google.com/android/repository/commandlinetools-linux-6609375_latest.zip
                        unzip commandlinetools-linux-6609375_latest.zip -d /var/lib/jenkins/tools/android-sdk
                    '''
                }
            }
        }
        stage('Archive APK') {
            steps {
                // Archive the APK file
                archiveArtifacts 'app/build/outputs/**/*.apk'
            }
        }
    }
}
