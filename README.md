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
