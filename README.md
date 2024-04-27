# Version, build, and deploy to AWS ECS with GitHub Actions

In this example we will use GitHub, GitHub Actions, AWS (IAM, ECR, ECS) to sematically version the repository `main` branch, build and push a versioned image with semver and latest tags into ECR, and then restart an ECS task to deploy the `latest` image.

## Table of Contents

- [Requirements](#requirements)
  - [AWS](#aws-account-with-proper-permissions-to)
  - [GitHub](#github-account-with-proper-permissions-to)
  - [Node.js](#nodejs)
- [GitHub](#github)
  - [Repository Settings](#repository-settings)
  - [Repository Secrets](#repository-secrets)
- [AWS](#aws)
  - [Identity and Access Management (IAM)](#identity-and-access-management-iam)
    - [User](#iam-user)
    - [Role](#iam-role)
  - [Elastic Container Registry (ECR)](#elastic-container-registry-ecr)
  - [Elastic Container Service (ECS)](#elastic-container-service-ecs)
    - [Create Cluster](#create-cluster)
    - [Define a Task](#define-a-task)
    - [Create a Service](#create-a-service)

## Requirements

### AWS account with proper permissions to

- Set proper IAM permissions
- Create and configure an ECR Repository
- Create and configure an ECS Cluster, Task Definitions and Services

### GitHub account with proper permissions to

- Create a repository
- Create secrets
- Create actions

### Node.js

Node.js is used to version the repository with a package.json file.

## GitHub

### Repository Settings

In GitHub go to the repository that you created and then go to Settings > Actions > General and make sure that "Workflow Permissions" are set to "Read and Write".

### Repository Secrets

In GitHub go to the repository you created for this project and then Settings > Secrets > Actions

These are the secrets you will need to set for your actions. You will get these values as you go through setting up and configuring the needed services.

- AWS_ACCESS_KEY_ID
- AWS_SECRET_ACCESS_KEY
- ECR_CLUSTER
- ECR_SERVICE
- REPO_NAME

## AWS

### Elastic Container Registry (ECR)

From the AWS console go to ECR for the region you want to work in and click "Create Repository".
Provide a name for the repository.
Note the ECR repository Name and AWS region for later use.

### Identity and Access Management (IAM)

#### IAM User

From the AWS console go to IAM then "Users" in the left hand navigation. You will need to create a user with the necessary permissions to access ECR and ECS.

Create a new user and set these permissions:

- AmazonEC2ContainerRegistryFullAccess
- ...

Add an Access Key to the IAM user and save the AWS Access Key ID and Secret Access Key for a future step.
Click on the user you want to add the access key to then go to Security Credentials > Access Keys > Create Access Key
...

#### IAM Role

Form the IAM Dashboard click on the Access Management > Roles link in the IAM sidebar.

- Click on "Create role" button. The trusted entity type should be "AWS Service"
- Use case should be Elastic Container Service - Elastic Container Service Task
- Click Next then seach find and check the box for:
  - AmazonECSTaskExecutionRolePolicy
  - ...
- Click Next and name the Role, for example: ecrecsdemo
- Click Create Role

### Elastic Container Service (ECS)

#### Create Cluster

- From the AWS console go to the ECS and click the "Create Cluster" button.
- Name the cluster and set the settings you want for your cluster.
  ...

#### Define a Task

- From the AWS ECS Dashboard click on the "Task Definitions" link in the ECS sidebar.
- Then click on the "Create new task definition" button.
- Set the settings you want but use the IAM Role you created for the "Task Role" and "Task Execution Role".
- Configure your "Infrastructure requirements" and your container settings.
- Click "Create" button

#### Create a Service

##### Network

VPC, Subnets & Security Group
...

#### Running your Task

- From the AWS ECS Dashboard click into the Cluster that you created.
- Click on the "Tasks" tab and then click on "Run new task"
- Select your compute configuration, I use "Launch type", "Fargate", "Latest"
- In the "Deployment Configuration" section select "Service"
- For "Family" select the task you created
- For "Revision" use LATEST
- Add a "Service Name" for example: ecrecsdemoservice
- Configure the other settings for your needs
- Click "Create"
