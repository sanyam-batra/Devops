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
        /*stage ('Build Stage') {

            steps {
                
                    sh 'mvn clean install'
                
            }
        }*/
	    stage('Build Docker image') {
		    steps{
         sh 'docker build -t demo-webapp:ver1 .'
     }
	    }
	    stage('Push image') {
	    steps {
                             
            
            withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: "DockerPass", usernameVariable: "DockerUser")])
                                 {
    
    
    
     sh "docker login -u $DockerUser -p $DockerPass"
            sh 'docker tag demo-webapp:ver1 sanyambatra/demo-webapp:ver1'
            sh 'docker push sanyambatra/demo-webapp:ver1'
            
				 }
				 }
         }


	 
}
}

    
 

    
