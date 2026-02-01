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
                // Ensure we run jacocoTestReport for the coverage data
                sh '/opt/gradle-8.5/bin/gradle clean build jacocoTestReport'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                // Using the token you provided from the SonarQube UI
                sh '/opt/gradle-8.5/bin/gradle sonar \
                    -Dsonar.login=sqp_1a15b5588c79e1d191bad741f0b2c9218597623b'
            }
        }
        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'build/libs/*.jar', fingerprint: true
            }
        }
    }
}
