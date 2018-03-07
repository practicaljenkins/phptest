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
  }

  post {
      failure {
        slackSend 'failed ${JOB_NAME} ${BUILD_NUMBER} (<${BUILD_URL}|Open>)'
      }
  }
}

