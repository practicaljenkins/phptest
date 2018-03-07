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
    stage('Create RPM') {
      steps {
        sh 'fpm -s ${WORKSPACE} -t rpm -a all -n ${JOB_BASE_NAME} -v 1.0 --iteration 1 src/=/var/www/${JOB_BASE_NAME} --exclude "var/www/${JOB_BASE_NAME}/Jenkinsfile"'
      }
    }
  }
}

