pipeline {
    agent any
    
    environment {
    	gitUrl = 'https://coenie.basson@git.telrock-labs.com/telrock-config/config-1stcredit.git'
    	jUnitPattern = '**/surefire-reports/*.xml'
    	jBehaveReportDir = 'telrock-tas-karma/target/jbehave/view'
    	jBehaveReportFiles = 'reports.html'
    	jBehaveReportName = 'JBehave - Karma'
    }
    
    stages {
    	stage('Checkout') {
		    steps {
			    git url: env.gitUrl, 
			        branch: env.buildBranch, 
			        credentialsId: 'eaf1e289-5cdf-4aa5-8490-041fc3a27097', 
			        poll: false    
		    }
		}

        stage ('Build') {
            steps {
            	sh 'mvn clean install'
            }
        }
        
        stage ('Publish jUnit tests') {
	        steps {
	        	junit allowEmptyResults: true, testResults: env.jUnitPattern      
	        } 	                      
        }
        
        stage ('Publish jBehave tests') {
        	steps {
        		publishHTML([
	 				allowMissing: true, 
	 				alwaysLinkToLastBuild: false, 
	 				keepAll: true, 
	 				reportDir: env.jBehaveReportDir, 
	 				reportFiles: env.jBehaveReportFiles, 
	 				reportName: env.jBehaveReportName, 
	 				reportTitles: '']) 
	        }                                        
        }
        
        stage ('Upload to Nexus') {
        	steps {
        		echo 'Loading to Nexus'     
        	}                     
        }
    }
}
