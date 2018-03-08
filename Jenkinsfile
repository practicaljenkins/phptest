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
        script{
          withCredentials([usernamePassword(credentialsId: 'jenkins-secret', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
            sh 'git checkout ${CHANGE_TARGET}'
            sh 'git merge --no-ff ${GIT_COMMIT}'
            sh 'git push origin ${CHANGE_TARGET}'
          }
        }
      }
    }
  }
}

