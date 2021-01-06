pipeline {
    agent any
    triggers {
        pollSCM '* * * * *'
    }
    stages {
        stage('Build') {
            steps {
                sh './gradlew build'
            }
        }
        stage('Test') {
            steps {
                sh './gradlew test'
            }
        }
        stage ('Sonarqube analysis') {
            steps {
                withSonarQubeEnv('Sonarqube') {
                    sh "./gradlew sonarqube"
                }
            }
        }
        stage ('Quality gate') {
            steps {
                waitForQualityGate abortPipeline: true
            }
        }
    }
}