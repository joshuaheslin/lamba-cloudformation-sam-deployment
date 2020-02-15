# AWS Lamba SAM Lamba Deployment with Scheduled Service

Boilerplate for creating/deploying an AWS lamba service with schedule cron expression service using SAM.

# Method 1 - Log in AWS account in command line

### 1 Log into aws cli

```
aws cli
aws configure
```

# Method 2 - SAM - Serverless Application Model

### 1 install aws-sam-cli

https://itnext.io/creating-aws-lambda-applications-with-sam-dd13258c16dd

```
pip install aws-sam-cli
```

### 2 Create sam version template (SAM templates extend Cloudformation)

Note must include the AWS:Serverless-2016-10-31 Transform key.
You don't need to touch anything here unless instructed.

This is `./deployment/template.yaml` file

### 3 Make a bucket first

```
aws s3 mb s3://sam-deployments-bucket
```

### 4 Package and Deploy it

Update the `deployment.yaml` file with the desired CRON expression

```
sam package --template-file ./deployment/template.yaml --output-template-file ./deployment/package.yaml --s3-bucket sam-deployments-bucket

sam deploy --template-file ./deployment/package.yaml --stack-name sam-deployment-boilerplate --capabilities CAPABILITY_IAM
```

### 5 Delete it

This will stop the entire service.

```
aws cloudformation delete-stack --stack-name sam-deployment-boilerplate
```