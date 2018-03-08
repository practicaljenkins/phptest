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
    stage('Merge PR') {
      when {
        branch 'PR-*'
      }
      steps {
        sshagent(['jenkins-ssh']) {
          sh 'git checkout ${CHANGE_TARGET}'
          sh 'git merge --no-ff ${GIT_COMMIT}'
          sh 'git push origin ${CHANGE_TARGET}'
        }
      }
    }
  }
}

