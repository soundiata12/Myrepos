pipeline{
    agent any
        
    
    stages{
        stage("Build job"){
            steps{
                script{
                    // This step should not normally be used in your script. Consult the inline help for details.
                        withDockerRegistry(url: 'https://646617499701.dkr.ecr.us-east-1.amazonaws.com/') {
                        sh "docker build -t myapp-revision ."
                        sh "docker tag myapp-revision:latest 646617499701.dkr.ecr.us-east-1.amazonaws.com/myapp-revision:latest"
                        sh "docker push 646617499701.dkr.ecr.us-east-1.amazonaws.com/myapp-revision:latest"
                }
            }
         }
     }
    }

}