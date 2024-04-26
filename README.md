# ECR ECS Example

In this example we will use GitHub actions to sematically version the repository main branch, create a docker image and push into ECR and then restart an ECS task to deploy the `latest` image.

## Requirements

- AWS account with proper permissions to
- Create and configure an ECR Repository
- Set proper IAM permissions
- Create and configure an ECS Cluster and Tasks
- GitHub account with proper permissions to
- Create a repository
- Create secrets
- Create actions

## GitHub Settings

### Repository Settings

In GitHub go to the repo that you created and then go to Settings > Actions > General and make sure that "Workflow Permissions" are set to "Read and Write".

### Secrets

In GitHub got to the repo and then Settings > Secrets > Actions

## AWS Settings

### ECR

Log into AWS and go to ECR for the region you want and click "Create Repository".
Provide a name for the repository.
Note down the ECR repository Name and AWS region for later use.

### IAM

Create an AWS Identity and Access Management (IAM) user with the necessary permissions to access the ECR repository. (Your IAM user must have “AmazonEC2ContainerRegistryFullAccess” IAM permissions)
Add an Access Key to that IAM user and save the AWS access key ID and secret access key for a future step.

### ECS
