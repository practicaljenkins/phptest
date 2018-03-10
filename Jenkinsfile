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
          def issue = jiraGetIssue idOrKey: env.GIT_BRANCH, site: 'practical-jenkins-jira'
          if (issue.code.toString() == '200') {
            response = jiraAddComment site: 'practical-jenkins-jira', idOrKey: env.GIT_BRANCH, comment: 'Build result: Job - env.JOB_NAME, Build number - env.BUILD_NUMBER, Build URL - env.BUILD_URL'
          } else {
            def issueInfo = [fields: [ project: [key: 'PJD'],
                             summary: 'Review build v1.1.0',
                             description: 'Review changes for build v1.1.0',
                             issuetype: [name: 'Task']]]
            response = jiraNewIssue issue: issueInfo, site: 'practical-jenkins-jira'
          }
        }
      }
    }
  }
}

