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
         sh 'sudo docker build -t demo-webapp:ver1 .'
     }

     stage('Push image') 
                             {
            
            withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: "DockerPass", usernameVariable: "DockerUser")])
                                 {
    
    
    
     sh "sudo docker login -u $DockerUser -p $DockerPass"
            sh 'sudo docker tag demo-webapp:ver1 sanyambatra/demo-webapp:ver1'
            sh ' sudo docker push sanyambatra/demo-webapp:ver1'
            
}
         }


	 
}
}

    
 

    
