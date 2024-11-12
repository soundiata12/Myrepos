pipeline{
    agent any
        
    
    stages{
        stage("Build ECR Repository"){
            steps{
                script{
                    // This step should not normally be used in your script. Consult the inline help for details.
                withDockerRegistry(credentialsId: 'ecr:us-east-1:Nafina-key', url: 'https://646617499701.dkr.ecr.us-east-1.amazonaws.com/') {
                 sh""
                }
              }
           }
        }
    }
}