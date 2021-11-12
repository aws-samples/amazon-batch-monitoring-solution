## CloudFormation template - Monitoring solution for AWS Batch jobs

This CloudFormation Template creates a monitoring solution for the AWS Batch Jobs in transit for more than "X" seconds before moving to RUNNING state. 

The solution consists of the following components created via CloudFormation:

- An Amazon CloudWatch event rule to monitor the submitted jobs in Batch using the target Lambda function
- An AWS Lambda function with the logic to monitor the submitted jobs and trigger Amazon Simple Notification Service (Amazon SNS) notifications
- A Lambda execution AWS Identity and Access Management (IAM) role
- An Amazon SNS topic to be subscribed by end users in order to be notified about the submitted jobs

## Requirements

- Python 3.9 runtime
- An AWS account
- An AWS Identity and Access Management (IAM) user authorized to use the AWS resources
- IAM roles for your AWS Batch compute environments and container instances
- AWS Batch resources – compute environment, job queue, and job definition
- AWS Batch jobs that would be monitored using this solution.

## How to use

Use the CloudFormation template 'MonitorBatchJobs.yaml' and create a CloudFormation stack on the AWS console. 

## Considerations

The Lambda function uses the ListJobs API call. The maximum number of results is returned by ListJobs in paginated output. Therefore, if you are submitting many jobs, then you must modify the Lambda function to fetch more results from the initial response of the call by using the nextToken response element. Use this nextToken element and iterate through in a loop to keep fetching the paginated results until there are no further nextToken elements present.

## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

// Copyright Amazon.com, Inc. or its affiliates. All Rights Reserved.

// SPDX-License-Identifier: MIT-0

