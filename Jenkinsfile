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
        sh './mvnw sonar:sonar -Dsonar.login=48b8d771792610fbe0e765d504110ef374344cb6'
      }
    }

    stage('Deploy') {
      steps {
        sh '/usr/bin/ansible-playbook /vagrant/ansible_devops.yml -i /vagrant/inventory -u vagrant --private_key=/var/tmp/my.key -f 5'
      }
    }

  }
}