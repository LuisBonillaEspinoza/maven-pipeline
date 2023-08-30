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
        stage('Test Maven - JUnit'){
              steps{
                  bat "mvn test"
              }
              post{
                  always{
                      junit 'target/surefire-reports/*.xml'
                  }
              }
        }
    }
}
