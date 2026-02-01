pipeline {
    agent any
    environment {
        // Replace with the output of 'pwd' in your gradle-8.5/bin folder
        GRADLE_HOME = '/home/cloud/gradle-demo/gradle-8.5'
        PATH = "${env.GRADLE_HOME}/bin:${env.PATH}"
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build & Test') {
            steps {
                // Now Jenkins will find the 'gradle' command
                sh 'gradle clean test' 
            }
        }
        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'build/libs/*.jar'
            }
        }
    }
}
