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

## AWS

### ECR

Log into AWS and go to ECR for the region you want and click "Create Repository".
Provide a name for the repository.
Note down the ECR repository Name and AWS region for later use.

### IAM

#### IAM User

Create an AWS Identity and Access Management (IAM) user with the necessary permissions to access the ECR repository. (Your IAM user must have “AmazonEC2ContainerRegistryFullAccess” IAM permissions)
Add an Access Key to that IAM user and save the AWS access key ID and secret access key for a future step.

#### IAM Role

Create an AWS Identity and Access Management (IAM) Role named "ecsTaskExecution".
Click on the Access Management > Roles link in the IAM sidebar.
Click on "Create role" button.
Trusted entity type should be "AWS Service"
Use case should be Elastic Container Service - Elastic Container Service Task
Click Next
Seach for and check the box for "AmazonECSTaskExecutionRolePolicy"
Click Next
Name the Role "ecrecsdemo"
Click Create Role

### ECS

#### Create Cluster

Go to the ECS Service in AWS and click the "Create Cluster" button.
Name the cluster and set the settings you want for your cluster.

#### Defining a Task

Click on the "Task Definitions" link in the ECS sidebar.
Then click on the "Create new task definition" button.
Set the settings you want but use the IAM Role you created for the "Task Role" and "Task Execution Role".
Configure your "Infrastructure requirements" and your container settings.
Click "Create" button

#### Creating a Service

##### Network

VPC, Subnets & Security Group
......

#### Running your Task

In ECS click into the Cluster that you created.
Click on "Tasks" tab and then click on "Run new task"
Select your compute configuration, I use "Launch type", Fargate, Latest
In "Deployment Configuration" select "Service"
For "Family" select the task you created
For "Revision" use LATEST
Add a "Service Name"
Set the "Desired tasks" amount and other settings
Click "Create"
