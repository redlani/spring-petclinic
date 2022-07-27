pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Building...'
        sh 'mvn clean install -Dlicense.skip=true'
      }
    }

    stage('Test') {
      parallel {
        stage('SonarQube') {
          steps {
            echo 'Initiating SonarQube test'
            sh 'mvn sonar:sonar -Dsonar.host.url=http://localhost:9000-Dlicense.skip=true'
          }
        }

        stage('Print Tester Credentials') {
          steps {
            echo "The tester is ${TESTER}"
          }
        }

        stage('Print Build Number') {
          steps {
            echo "This is build number ${BUILD_ID}"
          }
        }

      }
    }

  }
  environment {
    TESTER = 'Kailani'
    BUILD_ID = '1'
  }
}