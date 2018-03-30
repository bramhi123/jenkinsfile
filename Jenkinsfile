node {
  

   env.JAVA_HOME = tool 'JAVA_HOME'
  
   def mvnHome = tool 'M3'
  
  
   env.PATH = "${mvnHome}/bin:${env.JAVA_HOME}/bin:${env.PATH}"

  
 
   stage ('scm') {
    
   git 'https://github.com/bramhi123/helloworld-java-mavenproject.git'
   
   }
 
   stage("SonarQube analysis") {
          
   withSonarQubeEnv('SonarQube') {
                 
   sh 'mvn sonar:sonar'
              
   }
          
  }
  
   stage ('Compile or build Stage') {
            
            
   sh 'mvn clean compile'
        
   }
    
  

   stage ('Tesing Stage') {
        
        
   sh 'mvn test'
    
   }
     
   
 
   stage ('Package Stage') {
       
   sh 'mvn package'
   
   }  

      
  stage ('Distribute binaries to Jfrog Artifactory') { 
    def SERVER_ID = 'Jfrog' 
    def server = Artifactory.server SERVER_ID
    def uploadSpec = 
    """
    {
    "files": [
        {
            "pattern": "all/target/all-(*).jar",
            "target": "libs-release-local/"
        }
      ]
    }
    """
    def buildInfo = Artifactory.newBuildInfo() 
    buildInfo.env.capture = true 
    buildInfo=server.upload(uploadSpec) 
    server.publishBuildInfo(buildInfo) 
}    


}
