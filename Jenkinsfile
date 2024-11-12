pipeline{
    agent any
        parameters{
            string(name: 'MYAPP', defaultValue: '1.0.3')
        }
    
    stages{
        stage("Build ECR Repository"){
            steps{
                script{
                    // This step should not normally be used in your script. Consult the inline help for details.
                withDockerRegistry(credentialsId: 'ecr:us-east-1:Nafina-key', url: 'https://646617499701.dkr.ecr.us-east-1.amazonaws.com/') {
                 echo "Hello KEITA"
                 sh "docker build -t my-static-app:${params.MYAPP} ."
                 sh "docker tag my-static-app:${params.MYAPP} 646617499701.dkr.ecr.us-east-1.amazonaws.com/myapp-revision:${params.MYAPP}"
                 sh "docker tag my-static-app:${params.MYAPP} 646617499701.dkr.ecr.us-east-1.amazonaws.com/myapp-revision:latest" 
                 sh "docker push 646617499701.dkr.ecr.us-east-1.amazonaws.com/myapp-revision:latest"
                }
              }
           }
        }
    }
}