pipeline{
    agent any 
      
    stages{
        stage("sonar quality check"){   
            agent {
                docker {
                    image 'maven'
                    args '-u root'
                }
            }         
            steps{                
                script{
                    withSonarQubeEnv(credentialsId: 'sonar-token'){ 
                                         
                        sh 'mvn sonar:sonar'            
                        sh 'mvn clean package'                                    
                    }                     
                }  
            }            
        }
        stage("Quality gat status"){                      
            steps{                
                script{
                    withSonarQubeEnv(credentialsId: 'sonar-token'){ 
                        waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token' 
                    }                                  
                }                     
            }  
        }        
        // stage("docker build and push to Nexus repo"){                      
        //     steps{                
        //         script{
                                                     
        //         }                     
        //     }  
        // }       
    }
}
