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
                sh './gradlew clean build'
            }
        }

        stage('Archive Artifact') {
            steps {
                
                archiveArtifacts artifacts: 'build/libs/*.jar', fingerprint: true
            }
        }
        stage('SonarQube Analysis') {
         steps {
         script {
            withSonarQubeEnv('SonarQube') {
                sh "./mvnw sonar:sonar \
                    -Dsonar.projectKey=my-java-app \
                    -Dsonar.java.binaries=target/classes \
                    -Dsonar.coverage.jacoco.xmlReportPaths=target/site/jacoco/jacoco.xml"
            }
        }
    }
}
        
    }
 }

