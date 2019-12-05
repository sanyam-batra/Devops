pipeline {
    agent any

    stages {
	    stage('checkout scm') {
		    checkout scm
	    }
        stage ('Build Stage') {

            steps {
                withMaven(maven : 'maven_tool') {
                    sh 'mvn clean compile'
                }
            }
        }
    }
}

    
 

    
