This project outlines the steps to create a CI/CD pipeline using GitHub, Jenkins, Amazon Elastic Container Registry (ECR), and Amazon Elastic Container Service (ECS). The pipeline automates the process of triggering builds, deploying Docker images to ECR, and updating ECS services with the new images.

Steps

1. Configure GitHub Webhook

Task: Configure a webhook in your GitHub repository.

Purpose: Trigger Jenkins jobs whenever there is a push event in the GitHub repository.

2. Enable GitHub Hook Trigger in Jenkins

Task: Enable "GitHub hook trigger for GITScm polling" in Jenkins job configurations.

3. Test GitHub Webhook

Task: Verify that the webhook successfully triggers Jenkins jobs

4. Set Up Amazon Elastic Container Registry (ECR)

a. Create a User

Task: Create an AWS IAM user for ECR access.

b. Assign Credentials

Task: Generate an access key for the IAM user and save it securely.

c. Assign Permissions

Task: Grant the user the following permissions:

AmazonEC2ContainerRegistryFullAccess

AmazonECS_FullAccess

5. Configure Jenkins for AWS Integration

a. Install Plugins

Task: Install the following Jenkins plugins:

AWS Credentials

Amazon ECR

b. Create AWS Credentials

Inatall Trivy and Sonarqube

Task: Use the "AWS Credentials" option in Jenkins to create a credential in the "Kind" field.

c. Generate Pipeline Syntax

Task: Use Jenkins Pipeline Syntax to generate authentication code for AWS.

Instruction: Copy and paste the generated syntax into your Jenkinsfile.

6. Deploy Docker Images to ECR

a. Generate ECR Command

Task: Use the ECR command provided by AWS to push Docker images to the repository.

b. Add Command to Jenkins Job

Task: Copy the ECR command into your Jenkins job configuration

c. Test Deployment

Task: Verify that the Docker image is successfully deployed to ECR.

7. Configure Amazon Elastic Container Service (ECS)

a. Create ECS Cluster

Task: Create an ECS cluster and name it (e.g., clusterName).

b. Define Tasks

Task: Create a Task Definition for your application.

c. Create Service

Task: Create a service within the ECS cluster (e.g., serviceName).

8. Configure EC2 Instance for AWS CLI

a. Install AWS CLI

Task: Install AWS CLI on the EC2 instance using the following commands:

curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install

9. Jenkins Job for ECS Update

a. Create Jenkins Job

Task: Create a Jenkins job for updating ECS services

b. Add ECS Update Command

Task: Use the following command in the Jenkins job:

aws ecs update-service --cluster <clusterName> --service <serviceName> --force-new-deployment

Purpose: Trigger an ECS service update when new changes are pushed.
