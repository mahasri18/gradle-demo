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
                        withCredentials([(credentials: 'sonar-token', variable: 'SONAR-TOKEN')]){
                        sh '''
                        ./gradlew sonar \
                         -Dsonar.login=$SONAR_TOKEN
                         '''
                    }
                }
            }
        }
    }
 }
}
