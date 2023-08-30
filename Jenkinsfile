pipeline {
    agent any
    tools {
        maven "Maven"
    }

    stages {
        stage('Build Artifact') {
            steps {
                bat "mvn clean package -DskipTests=true"
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }
}
