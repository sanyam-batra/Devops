pipeline {
    agent any
	def dockerHome = tool 'docker_tool'
	tools {
		maven 'maven_tool'
		
	}
	environment {
    registry = "sanyambatra/demo-pipeline"
    registryCredential = 'dockerhub'
    dockerimage= ''
}

    stages {
	    stage('checkout scm') {
		    steps{
			    
		    checkout scm
		    }
	    }
        /*stage ('Build Stage') {

            steps {
                
                    sh 'mvn clean install'
                
            }
        }*/
	    stage('Building image') {
		    
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
	        stage('Deploy Image') {
			
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }

    }
}

    
 

    
