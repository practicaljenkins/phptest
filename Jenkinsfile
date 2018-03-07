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
    stage('SonarQube analysis') {
      steps {
        withSonarQubeEnv('Practical Jenkins Sonarqube') {
          sh 'echo "sonar.projectKey=production:phptest" > ${WORKSPACE}/sonar-project.properties'
          sh 'echo "sonar.sources=." >> ${WORKSPACE}/sonar-project.properties'
          sh '/opt/sonarqube-scanner/bin/sonar-scanner'
        }
      }
    }
  }
}

