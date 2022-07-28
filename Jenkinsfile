pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        echo 'Checking out repo'
//         checkout steps here
      }
    }

    stage('Build') {
      steps {
        echo 'Attempting build'
        sh './mvnw clean install -DskipTests'
      }
    }
    
    stage('Scan') {
      steps {
        echo 'Attempting SonarQube Analysis'
        withSonarQubeEnv(installationName: 'sq1') {
            sh './mvnw clean install sonar:sonar'
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
