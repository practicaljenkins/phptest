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
    stage('PHPUnit Test') {
      steps {
        echo 'Running PHPUnit...'
        sh '/bin/phpunit ${WORKSPACE}'
        sh 'sed -i "s/https:\/\/github.com\//git@github.com:/" ${WORKSPACE}/.git/config'
      }
    }
  }
}

