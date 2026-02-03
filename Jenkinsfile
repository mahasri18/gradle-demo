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
                // Update the projectKey and projectName here
                sh "./gradlew sonar \
                    -Dsonar.projectKey=gradle-demo \
                    -Dsonar.projectName='gradle-demo' \
                    -Dsonar.java.binaries=build/classes \
                    -Dsonar.coverage.jacoco.xmlReportPaths=build/reports/jacoco/test/jacocoTestReport.xml"
            }
        }
    }
}
        
    }
 }

