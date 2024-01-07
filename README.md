# AWS AutoMLOps Serverless Deployment

[![🧩 Serverless deployment to AWS](https://github.com/kwame-mintah/aws-automlops-serverless-deployment/actions/workflows/serverless-deploy.yml/badge.svg)](https://github.com/kwame-mintah/aws-automlops-serverless-deployment/actions/workflows/serverless-deploy.yml)

This repository contains the serverless deployment yaml for lambda functions used to achieve MLOps Level 2 within AWS. Not all resources
are created by this deployment in AWS, some resources are created via the [terraform-aws-machine-learning-pipeline](https://github.com/kwame-mintah/terraform-aws-machine-learning-pipeline) repository.

The lambda functions deployed aim to automate, preparing data and transforming features, training and tuning, deploying models and running inferences etc.

# Architecture

![](/docs/drawio/aws-automlops-deployment.png)

1. User has received new data.
2. Data is uploaded to a GitHub repository.
3. A GitHub action is triggered uploading the data to an S3 Bucket.
4. Lambda function for data preprocessing is run due to an event trigger on the bucket.

## GitHub Action (CI/CD)

The GitHub Action will deploy the lambda functions using the [serverless](https://github.com/serverless/github-action) action. Docker images used for deployment are stored
within an AWS ECR repository.
