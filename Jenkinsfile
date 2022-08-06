pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        echo 'Checking out repo'
      }
    }

    stage('Build') {
      steps {
        echo 'Attempting build'
        sh './mvnw package'
      }
    }

    stage('Scan') {
      steps {
        echo 'Attempting SonarQube Analysis'
        withSonarQubeEnv('sq1') {
          sh './mvnw sonar:sonar'
        }

      }
    }

    stage('Run') {
      steps {
        sh 'java -jar target/*.jar'
      }
    }

  }
}