# AWS AutoMLOps Serverless Deployment

[![🧩 Serverless deployment to AWS](https://github.com/kwame-mintah/aws-automlops-serverless-deployment/actions/workflows/serverless-deploy.yml/badge.svg)](https://github.com/kwame-mintah/aws-automlops-serverless-deployment/actions/workflows/serverless-deploy.yml)
[![💥 Serverless remove resources](https://github.com/kwame-mintah/aws-automlops-serverless-deployment/actions/workflows/serverless-remove.yml/badge.svg)](https://github.com/kwame-mintah/aws-automlops-serverless-deployment/actions/workflows/serverless-remove.yml)

This repository contains the serverless deployment yaml for lambda functions used to achieve MLOps Level 2 within AWS. Not all resources
are created by this deployment in AWS, some resources are created via the [terraform-aws-machine-learning-pipeline](https://github.com/kwame-mintah/terraform-aws-machine-learning-pipeline) repository.

The lambda functions deployed aim to automate, preparing data and transforming features, training and tuning, deploying models and running inferences etc.

# Architecture

![](/docs/drawio/aws-automlops-deployment.png)

1. User has received new data.
2. Data is uploaded to a GitHub repository.
3. A GitHub action is triggered uploading the data to an S3 Bucket.
4. Lambda function for data preprocessing is run due to an event trigger on the bucket.
5. Upon completion the transform data is uploaded to another bucket.
6. Lambda function to start the training job is started due to an event trigger on the bucket.
7. Training job is started using data split for train, test and validation purposes.
8. Completed model is uploaded to an S3 Bucket.
9. Lambda function to deploy the new model for inference and evaluation etc.

## Lambda repositories

The source code for all lambda functions are stored in GitHub:
- dataPreProcessing: [aws-lambda-data-preprocessing](https://github.com/kwame-mintah/aws-lambda-data-preprocessing)

## GitHub Action (CI/CD)

The GitHub Action will deploy the lambda functions using the [serverless](https://github.com/serverless/github-action) action. Docker images used for deployment are stored
within an AWS ECR repository.
