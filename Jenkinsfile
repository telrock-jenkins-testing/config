pipeline {
  agent any
  stages {
    stage('checkout') {
      steps {
        git(url: 'https://coenie.basson@git.telrock-labs.com/telrock-config/config-1stcredit.git', branch: 'rc/1.9.0-SNAPSHOT', changelog: true)
      }
    }
    stage('Build') {
      steps {
        sh 'mvn clean install'
      }
    }
    stage('') {
      steps {
        junit(allowEmptyResults: true, testResults: '**/surefire-reports/*.xml', healthScaleFactor: 1)
      }
    }
    stage('Load to nexus') {
      steps {
        echo 'Still to do'
      }
    }
  }
}