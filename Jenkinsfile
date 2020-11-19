pipeline {
    agent none
    stages {
        stage("build & SonarQube analysis") {
            agent any
            steps {
                withSonarQubeEnv('dmeppiel_sq') {
                    sh 'sonar-scanner'
                }
            }
        }
        stage("Quality Gate") {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}