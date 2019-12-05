pipeline {
    agent any
	tools {
		maven 'maven_tool'
		docker 'docker_tool'
	}
	environment {
    registry = "sanyambatra/demo-pipeline"
    registryCredential = ‘docker-hub’
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

    
 

    
