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
        sh 'git remote set-url origin git@github.com:practicaljenkins/phptest.git'
      }
    }
    stage('JIRA') {
      steps {
        withEnv(['JIRA_SITE="practical-jenkins-jira"']) {
          script {
            def issue = [fields: [ project: [key: 'PJD'],
                               summary: 'Release 1.2.0',
                               description: 'Review changes for release 1.2.0',
                               issuetype: [name: 'Task']]]
            def newIssue = jiraNewIssue issue: issue
          }
        }
      }
    }
  }
}

