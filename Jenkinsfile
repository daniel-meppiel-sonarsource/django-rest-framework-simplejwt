pipeline {
    agent none
    stages {
        stage("build & SonarQube analysis") {
            agent any
            def scannerHome = tool 'SQ_Scanner_Latest';
            steps {
                withSonarQubeEnv('dmeppiel_sq') {
                    sh "${scannerHome}/bin/sonar-scanner"
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