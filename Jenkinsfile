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
                // Use your verified credentials: admin / cloud
                sh '/opt/gradle-8.5/bin/gradle sonar \
                    -Dsonar.host.url=http://localhost:9000 \
                    -Dsonar.login=admin \
                    -Dsonar.password=cloud'
            }
        }
        stage('Archive Artifact') {
            steps { archiveArtifacts artifacts: 'build/libs/*.jar' }
        }
    }
}
