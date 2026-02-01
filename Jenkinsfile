pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps { checkout scm }
        }
        stage('Build & Test') {
            steps {
                // We add jacocoTestReport to ensure the XML is ready for Sonar
                sh '/opt/gradle-8.5/bin/gradle clean build jacocoTestReport'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                // 'SonarQube' must match your Jenkins Global Tool Config name
                withSonarQubeEnv('SonarQube') {
                    sh '/opt/gradle-8.5/bin/gradle sonar'
                }
            }
        }
        stage('Archive Artifact') {
            steps { archiveArtifacts artifacts: 'build/libs/*.jar' }
        }
    }
}
