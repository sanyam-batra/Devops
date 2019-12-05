pipeline {
    agent any
	tools {
		maven 'maven_tool'
	}

    stages {
	    stage('checkout scm') {
		    steps{
			    
		    checkout scm
		    }
	    }
        stage ('Build Stage') {

            steps {
                
                    sh 'mvn clean install'
                
            }
        }
    }
}

    
 

    
