pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        echo "Checking out ${env.gitUrl} ${env.buildBranch}"
        git(url: env.gitUrl, branch: env.buildBranch, credentialsId: 'eaf1e289-5cdf-4aa5-8490-041fc3a27097', poll: true, changelog: true)
      }
    }
    stage('Build') {
      steps {
        sh 'mvn clean install'
      }
    }
    stage('Upload to Nexus') {
      steps {
        echo 'Loading to Nexus'
      }
    }
  }
  environment {
    gitUrl = 'https://coenie.basson@git.telrock-labs.com/telrock-config/config-1stcredit.git'
    buildBranch = 'rc/**'
    jUnitPattern = '**/surefire-reports/*.xml'
    jBehaveReportDir = 'telrock-tas-karma/target/jbehave/view'
    jBehaveReportFiles = 'reports.html'
    jBehaveReportName = 'JBehave - Karma'
  }
  post {
    always {
      echo 'Publishing jUnit test results'
      junit(allowEmptyResults: true, testResults: env.jUnitPattern)
      echo 'Publishing jBehave test results'
      junit(allowEmptyResults: true, testResults: env.jUnitPattern)
      publishHTML(allowMissing: true, alwaysLinkToLastBuild: false, keepAll: true, reportDir: env.jBehaveReportDir, reportFiles: env.jBehaveReportFiles, reportName: env.jBehaveReportName, reportTitles: '')
      
    }
    
  }
}