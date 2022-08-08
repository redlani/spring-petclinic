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
        sh './mvnw sonar:sonar -Dsonar.login=5adb862cef588f0c90aaf2c7436a158b23d56cd7'
      }
    }

    stage('Deploy') {
      steps {
        sh '/usr/bin/ansible-playbook /vagrant/ansible_devops.yml -i /vagrant/inventory -u vagrant --private-key=/var/tmp/my.key -f 5'
      }
    }

  }
}
