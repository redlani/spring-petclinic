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
        sh './mvnw clean install -DskipTests'
      }
    }
    
    stage('Scan') {
      steps {
        echo 'Attempting SonarQube Analysis'
        withSonarQubeEnv(installationName: 'sq1') {
            sh 'mvn sonar:sonar \
                  -Dsonar.projectKey=spring-petclinic-jenkins \
                  -Dsonar.host.url=http://10.0.2.15:9000 \
                  -Dsonar.login=239dc0527daa08ffd25e8fbf8c638cf25e80ed11'
        }

      }
    }

    stage('Run') {
      steps {
        sh './mvnw package'
        sh 'java -jar target/*.jar'
      }
    }

  }
}
