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
        sh '/usr/local/bin/fpm -s dir -t rpm -a all -n phptest -v 1.0 --iteration 1 ${WORKSPACE}/src/=/var/www/phptest'
      }
    }
  }

  post {
      always {
        cleanWs notFailBuild: true
      }
  }
}

