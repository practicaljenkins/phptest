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
      }
    }
  }
}

