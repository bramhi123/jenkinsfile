node {
  

   env.JAVA_HOME = tool 'JAVA_HOME'
  
   def mvnHome = tool 'M3'
  
  
   env.PATH = "${mvnHome}/bin:${env.JAVA_HOME}/bin:${env.PATH}"

  
 
   stage ('scm') {
    
   git 'https://github.com/bramhi123/helloworld-java-mavenproject.git'
   
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

    
 
   stage("SonarQube analysis") {
          
   withSonarQubeEnv('SonarQube') {
                 
   sh 'mvn sonar:sonar'
              
 }
          
}
      
      
}
