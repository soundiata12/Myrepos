pipeline {
    agent any

    parameters {
        string(name: 'MYAPP', defaultValue: '1.0.3')
    }

    environment {
        ECR_REPO_URL = '646617499701.dkr.ecr.us-east-1.amazonaws.com' // This variable refers to the link of the ECR repository
        APP_NAME = 'my-static-app' // This variable is used to give the name of my image in my current Docker (EC2 instance)
        ECR_REPO_NAME = 'mycloud_repo' // This variable is used to give the name of my image in ECR
        CRED_ID = 'ecr:us-east-1:Nafina-key' // This variable refers to my AWS credential
        ECS_CLUSTER_NAME = 'mycluster' // My ECS cluster name
        ECS_SERVICE = 'myapp' // My ECS service name
        MY_URL = "https://${ECR_REPO_URL}/"
        SCANER_SNANER= tool 'my_tool_sonar'
        SONAR_NAME= 'mystaticapp'
    }

    stages {

        stage("Sonarqube Scan"){
            steps{
                script {
                  withSonarQubeEnv('my_server_sonar') {
                 // some block
                    
                     sh '''
                 ${SCANER_SNANER}/bin/sonar-scanner \
                  -Dsonar.projectKey=${SONAR_NAME} \
                  -Dsonar.sources=. \
                  -Dsonar.projectName=${SONAR_NAME} \
                  -Dsonar.java.binaries=. 
                    '''
                 }
            }
            
        }
    }
        stage("Scan the file") {
            steps {
                sh "trivy fs --format table -o mystatic_app.html ."
            }
        }

        

        stage('Build image') {
            steps {
                script {
                    echo "Hello KEITA"
                    sh "docker build -t ${APP_NAME}:${params.MYAPP} ."
                    sh "docker tag ${APP_NAME}:${params.MYAPP} ${ECR_REPO_URL}/${ECR_REPO_NAME}:${params.MYAPP}"
                    sh "docker tag ${APP_NAME}:${params.MYAPP} ${ECR_REPO_URL}/${ECR_REPO_NAME}:latest"
                }
            }
        }

        stage("Scan image build") {
            steps {
                sh "trivy image --format table -o docker_image_mystatic_app.html ${ECR_REPO_URL}/${ECR_REPO_NAME}:latest"
            }
        }

        stage('Push in ECR Repository') {
            steps {
                script {
                    // This step should not normally be used in your script. Consult the inline help for details.
                    withDockerRegistry(credentialsId: CRED_ID, url: MY_URL) {
                        sh "docker push ${ECR_REPO_URL}/${ECR_REPO_NAME}:latest"
                        sh "docker push ${ECR_REPO_URL}/${ECR_REPO_NAME}:${params.MYAPP}"
                    }
                }
            }
        }

        stage("Update ECS") {
            steps {
                sh "aws ecs update-service --cluster ${ECS_CLUSTER_NAME} --service ${ECS_SERVICE} --force-new-deployment"
            }
        }
    }
}
   