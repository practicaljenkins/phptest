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
      }
    }
    stage('View ENV variables') {
      steps {
        echo '${BRANCH_NAME} ${CHANGE_ID} ${CHANGE_TARGET}'
      }
    }
  }

}

