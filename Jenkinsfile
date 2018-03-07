pipeline {

  agent {
    node {
      label 'master'
    }
  }

  options {
    timestamps()
  }

  stages {
    stage('Build') {
      parallel {
        stage('PHPUnit Test') {
          steps {
            echo 'Running PHPUnit...'
            sh '/bin/phpunit ${WORKSPACE}'
          }
        }
        stage('SonarQube analysis') {
          def scannerHome = tool 'Sonarqube Scanner'
          withSonarQubeEnv('Practical Jenkins SonarQube') {
            sh "${scannerHome}/bin/sonar-scanner"
          }
        }
      }
    }
  }
}

