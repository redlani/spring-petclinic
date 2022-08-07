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
        sh './mvnw package -Dmaven.test.skip'
      }
    }

    stage('Scan') {
      steps {
        echo 'Attempting SonarQube Analysis'
        mvn sonar:sonar \
          -Dsonar.projectKey=spring-petclinic-jenkins \
          -Dsonar.host.url=http://192.168.50.4:9000 \
          -Dsonar.login=40e4ddd255c2ef5098f90250ca7addf126706c7f
//         withSonarQubeEnv('sq1') {
//           sh './mvnw sonar:sonar'
//         }
      }
    }

    stage('Run') {
      steps {
        sh 'java -jar target/*.jar'
      }
    }

  }
}
