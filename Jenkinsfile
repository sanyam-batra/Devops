
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
        //rtMaven.deployer releaseRepo: ' example-repo-local', snapshotRepo: ' example-repo-local', server: server
        rtMaven.resolver releaseRepo: ' example-repo-local', snapshotRepo: ' example-repo-local', server: server
	
        buildInfo = Artifactory.newBuildInfo()
        buildInfo.env.capture = true
	
    }

    stage ('Exec Maven') {
        rtMaven.run pom: 'pom.xml', goals: '-U clean install', buildInfo: buildInfo
    }

    stage ('Publish build info') {
        server.publishBuildInfo buildInfo
    }
    
   
}

    
 

    
