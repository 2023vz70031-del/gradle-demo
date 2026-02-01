pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build & Test') {
            steps {
                // Use 'gradle' since it is in your Linux PATH
                sh 'gradle clean test' 
            }
        }
        stage('Archive Artifact') {
            steps {
                // This archives the JAR file so it appears in the Jenkins UI
                archiveArtifacts artifacts: 'build/libs/*.jar', fingerprint: true
            }
        }
    }
}
