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
        stage('Test Maven - JUnit') {
            steps {
                bat "mvn test"
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Sonarqube Analysis - SAST') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    bat """mvn sonar:sonar \
                        -Dsonar.projectKey=maven-pipeline \
                        -Dsonar.host.url=http://localhost:9000"""
                }
            }
        }
        stage("Sonatqube Analysis"){
            steps {
                script{
                    def scannerHome = tool 'SonarQube'
                    withSonarQubeEnv('SonarQube') {
                        bat "${scannerHome}/bin/sonar-scanner"
                    }
                }
            }
        }
    }
}
