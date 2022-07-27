pipeline {
    agent any
    tools {
        maven 'M3'
    }

    stages {
        stage('Checkout') {
            steps {
                // checkout the repo using the correct credentials
                git branch: 'main', credentialsId: 'git-token', url: 'https://github.com/redlani/spring-petclinic.git'
            }
        }
        stage('Scan') {
            steps {
                withSonarQubeEnv(installationName: 'sq1') {
                    sh'./mvn clean org.sonarsource.scanner.maven.sonar-maven-plugin:3.9.0.2155:sonar'
                }
            }
        }
        stage('Build') {
            steps {
                sh 'mvn compile'
                }
            }
        }
    }
}