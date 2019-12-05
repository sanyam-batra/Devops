pipeline {
    agent any
	tools {
		maven 'maven_tool'
		docker 'docker_tool'
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
	    stage('Build and push image') {
		    steps {
			    sh 'sudo docker build -t demo-webapp:ver1 .'
			    withCredentials([usernamePassword(credentialsId: 'docker-hub', passwordVariable: "DockerPass", usernameVariable: "DockerUser")])
                                 {
    
    
    
    
     sh "sudo docker login -u $DockerUser -p $DockerPass"
            sh 'sudo docker tag demo-webapp:ver1 sanyambatra13/demo-webapp:ver1'
            sh ' sudo docker push sanyambatra13/demo-webapp:ver1'
            
}
		    }
	    }
    }
}

    
 

    
