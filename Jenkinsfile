node {
    
    def server = Artifactory.server 'artifactory'
    def rtMaven = Artifactory.newMavenBuild()
    
    def buildInfo
    def mvnHome
    jdk = tool name: 'JAVA8'
    env.JAVA_HOME = "${jdk}"
    
    stage ('checkout scm') {
    checkout scm
    }
    stage ('Artifactory configuration') {
        mvnHome = tool 'mavenhome'
        rtMaven.tool = 'mavenhome' // Tool name from Jenkins configuration
        rtMaven.deployer releaseRepo: 'libs-release-local', snapshotRepo: 'libs-snapshot-local', server: server
        rtMaven.resolver releaseRepo: 'libs-release', snapshotRepo: 'libs-snapshot', server: server
        buildInfo = Artifactory.newBuildInfo()
        buildInfo.env.capture = true
    }

    /*stage ('Exec Maven') {
        rtMaven.run pom: 'pom.xml', goals: 'clean install', buildInfo: buildInfo
    }

    stage ('Publish build info') {
        server.publishBuildInfo buildInfo
    }
     stage('SonarQube analysis') {
         mvnHome = tool 'mavenhome'
    withSonarQubeEnv('sonar') {
      // requires SonarQube Scanner for Maven 3.2+
      rtMaven.run pom: 'pom.xml', goals: 'clean package sonar:sonar', buildInfo: buildInfo
    }
     } */
  
  stage('Build Docker image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line 
         app = docker.build("sanyambatra13/maven-demo") */
         sh 'sudo docker build -t jenkins-webapp:ver1 .'
     }

     stage('Push image') 
                             {
                                 
                             /* Finally, we'll push the image with two tags:
                                           * First, the incremental build number from Jenkins
                                           * Second, the 'latest' tag.
                                           * Pushing multiple tags is cheap, as all the layers are reused. 
                                           
                                          sudo docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
            sudo app.push("${env.BUILD_NUMBER}")
            sudo app.push("latest")*/
            
            withCredentials([usernamePassword(credentialsId: 'docker-hub', passwordVariable: "DockerPass", usernameVariable: "DockerUser")])
                                 {
    // some block
    
    
    
     sh "sudo docker login -u $DockerUser -p $DockerPass"
            sh 'sudo docker tag jenkins-webapp:ver1 sanyambatra13/jenkins-webapp:ver1'
            sh ' sudo docker push sanyambatra13/jenkins-webapp:ver1'
            
}
         }
     stage('Terraform') {
    

         sh 'terraform init'
         withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'SanyamAWS', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
        sh 'terraform apply -auto-approve'
  

      }
     }
    
    
    
    stage('connection') {   
	               
	        sshagent(['Sanyamsec']) {
	    
	             sh 'ssh -o StrictHostKeyChecking=no ubuntu@ec2-3-86-104-43.compute-1.amazonaws.com'
                     
	            sh 'ssh ubuntu@ec2-3-86-104-43.compute-1.amazonaws.com pwd'
			
			
		 
   

		    
	            /*sh 'ssh ubuntu@ec2-3-86-104-43.compute-1.amazonaws.com echo "if [  "$(docker ps -q -f name=sanyam)" ]; then docker kill sanyam docker rm sanyam fi docker pull sanyambatra13/jenkins-webapp:ver1 docker run --name sanyam -d -p 8888:8888 sanyambatra13/jenkins-webapp:ver1">>dockerexec.sh'
	            sh 'ssh ubuntu@ec2-3-86-104-43.compute-1.amazonaws.com ./dockerexec.sh'*/
			
		    /*sh 'ssh ubuntu@ec2-3-86-104-43.compute-1.amazonaws.com sudo docker ps -f name=sanyam -q | xargs --no-run-if-empty docker container stop'
		    sh 'ssh ubuntu@ec2-3-86-104-43.compute-1.amazonaws.com sudo docker container ls -a -fname=sanyam -q | xargs -r docker container rm'*/
		    
		    
	             sh 'ssh ubuntu@ec2-3-86-104-43.compute-1.amazonaws.com sudo docker pull sanyambatra13/jenkins-webapp:ver1' 
		    	
	             sh 'ssh ubuntu@ec2-3-86-104-43.compute-1.amazonaws.com sudo docker run --name sanyam-currentBuild.number -d -p 8888:8888 sanyambatra13/jenkins-webapp:ver1'
	            }      
	            
    }
    
    
    
}
    
 

    
