pipeline {
    agent any
	
	tools {
		maven 'maven_tool'
		
	}
	environment {
    	registry = "sanyambatra/demo-pipeline"
    	registryCredential = 'docker-hub'
	dockerImage = ''
		
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
	    stage('Build Docker image') {
		    steps{
		    script {
          dockerImage=docker.build registry + ":$BUILD_NUMBER"
        }
     }
	    }
	    stage('Push image') {
	    steps {
                          script {
      docker.withRegistry( '', registryCredential ) {
        dockerImage.push()
      }   
 
				 }
         }


	 
}
}
}
    
 

    
