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
    stage('JIRA') {
      steps {
        script {
          def issueInfo = [fields: [ project: [key: 'PJD'],
                             summary: 'Release 1.2.0',
                             description: 'Review changes for release 1.2.0',
                             issuetype: [name: 'Task']]]
          response = jiraNewIssue issue: issueInfo, site: 'practical-jenkins-jira'
          echo response.data.toString()
        }
      }
    }
  }
}

