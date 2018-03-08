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
    stage('View ENVs') {
      steps {
        sh 'echo ${BRANCH_NAME}'
        sh 'echo ${CHANGE_ID}'
        sh 'echo ${CHANGE_TARGET}'
        sh 'echo ${GIT_URL}'
        sh 'echo ${JOB_NAME}'
      }
    }
  }
}

