# AWS Automated Cost Optimizer

## Project Overview

This project demonstrates how to automate AWS cost optimization using AWS Lambda, Amazon EventBridge, IAM, and Amazon EC2.

The solution automatically checks running EC2 instances and stops them on a scheduled basis, helping reduce unnecessary AWS costs.

## Architecture

EventBridge → AWS Lambda → Amazon EC2

## AWS Services Used

* AWS Lambda
* Amazon EventBridge
* Amazon EC2
* AWS IAM
* Amazon CloudWatch Logs

## Project Workflow

1. EventBridge triggers the Lambda function every 5 minutes.
2. Lambda checks running EC2 instances.
3. Lambda stops running instances automatically.
4. CloudWatch Logs store execution logs.

## Lambda Function Code

```python
import boto3

ec2 = boto3.client('ec2')

def lambda_handler(event, context):

    instances = ec2.describe_instances()

    for reservation in instances['Reservations']:
        for instance in reservation['Instances']:

            instance_id = instance['InstanceId']

            state = instance['State']['Name']

            if state == 'running':
                ec2.stop_instances(
                    InstanceIds=[instance_id]
                )

                print(f"Stopped {instance_id}")

    return {
        'statusCode': 200,
        'body': 'Optimization Complete'
    }
```

## Screenshots

### Lambda Function Overview

Add screenshot here

### Lambda Code

Add screenshot here

### EventBridge Trigger

Add screenshot here

### Successful Test Execution

Add screenshot here

### IAM Permissions

Add screenshot here

### EC2 Instance Status

Add screenshot here

## Results

* Automated EC2 instance management
* Reduced unnecessary AWS resource usage
* Implemented serverless automation using AWS services
* Improved understanding of AWS Lambda, IAM, EventBridge, and EC2

## Author

Priyanka Dalavi

Aspiring AWS Cloud Engineer
