# AWS CloudFormation

## Table of Contents

1.  [Introduction to AWS CloudFormation](#introduction-to-aws-cloudformation)
2.  [Creating a CloudFormation Template](#creating-a-cloudformation-template)
3.  [Setting Up a CloudFormation Stack](#setting-up-a-cloudformation-stack)
4.  [Managing Changes with Change Sets](#managing-changes-with-change-sets)
5.  [Sample Template: DynamoDB and IAM Role](#sample-template-dynamodb-and-iam-role)
6.  [Conclusion and Key Metrics](#conclusion-and-key-metrics)

## Introduction to AWS CloudFormation

AWS CloudFormation is a powerful tool that allows you to define and provision AWS infrastructure as code. By creating templates, you can automate the creation and management of AWS resources, ensuring consistent and repeatable deployments.

## Creating a CloudFormation Template

A CloudFormation template is a JSON or YAML file that describes the AWS resources you want to create. YAML is commonly used due to its readability and community preference.

### Example: DynamoDB Table and IAM Role

yaml

Copy code

`AWSTemplateFormatVersion: '2010-09-09'
Resources:
OrdersTable:
Type: "AWS::DynamoDB::Table"
Properties:
TableName: "Orders"
AttributeDefinitions: - AttributeName: "OrderID"
AttributeType: "S"
KeySchema: - AttributeName: "OrderID"
KeyType: "HASH"
ProvisionedThroughput:
ReadCapacityUnits: 5
WriteCapacityUnits: 5

DynamoDBQueryPolicy:
Type: "AWS::IAM::Policy"
Properties:
PolicyName: "DynamoDBQueryPolicy"
PolicyDocument:
Version: "2012-10-17"
Statement: - Effect: "Allow"
Action: "dynamodb:Query"
Resource: "\*"
Roles: - Ref: "DynamoDBQueryRole"

DynamoDBQueryRole:
Type: "AWS::IAM::Role"
Properties:
AssumeRolePolicyDocument:
Version: "2012-10-17"
Statement: - Effect: "Allow"
Principal:
Service: "ec2.amazonaws.com"
Action: "sts:AssumeRole"`

## Setting Up a CloudFormation Stack

### Steps to Create a Stack

1.  **Open AWS CloudFormation Console**: Navigate to the CloudFormation section in the AWS Management Console.
2.  **Create a New Stack**: Click on "Create stack" and choose "With new resources".
3.  **Upload Template**: Select the option to upload a template file and choose your template (e.g., `dynamotemplate.yml`).
4.  **Configure Stack Settings**: Provide a stack name, such as `DynamoDBDemo`, and configure any additional settings if necessary.
5.  **Create Stack**: Review your settings and click "Create stack". CloudFormation will create the resources defined in your template.

## Managing Changes with Change Sets

Change Sets allow you to modify existing CloudFormation stacks without immediate execution. This feature is useful for previewing changes and ensuring they won't disrupt your resources.

### Steps to Create and Apply a Change Set

1.  **Modify Template**: Make changes to your template file (e.g., update `ProvisionedThroughput` from 5 to 10).
2.  **Create Change Set**: In the CloudFormation console, select your stack, choose "Stack actions", and click "Create change set for current stack".
3.  **Upload Updated Template**: Upload the modified template file and review the changes.
4.  **Execute Change Set**: After reviewing, execute the change set to apply the changes.

## Sample Template: DynamoDB and IAM Role

Below is a sample template that defines a DynamoDB table and an IAM role with a policy to query the table.

### Template File: `dynamotemplate.yml`

yaml

Copy code

`AWSTemplateFormatVersion: '2010-09-09'
Resources:
OrdersTable:
Type: "AWS::DynamoDB::Table"
Properties:
TableName: "Orders"
AttributeDefinitions: - AttributeName: "OrderID"
AttributeType: "S"
KeySchema: - AttributeName: "OrderID"
KeyType: "HASH"
ProvisionedThroughput:
ReadCapacityUnits: 5
WriteCapacityUnits: 5

DynamoDBQueryPolicy:
Type: "AWS::IAM::Policy"
Properties:
PolicyName: "DynamoDBQueryPolicy"
PolicyDocument:
Version: "2012-10-17"
Statement: - Effect: "Allow"
Action: "dynamodb:Query"
Resource: "\*"
Roles: - Ref: "DynamoDBQueryRole"

DynamoDBQueryRole:
Type: "AWS::IAM::Role"
Properties:
AssumeRolePolicyDocument:
Version: "2012-10-17"
Statement: - Effect: "Allow"
Principal:
Service: "ec2.amazonaws.com"
Action: "sts:AssumeRole"`

## Conclusion and Key Metrics

AWS CloudFormation simplifies infrastructure management by allowing you to define resources as code. This tutorial covered the basics of creating templates, setting up stacks, and managing changes. By following these steps, you can ensure consistent and repeatable deployments of your AWS resources.

### Key Metrics

- **Template Language**: YAML
- **Resource Types**: DynamoDB, IAM
- **Provisioning Time**: Approximately 2-3 minutes per stack creation
- **Change Set Time**: Varies based on changes, typically less than 1 minute for small updates

Explore further features of AWS CloudFormation to enhance your infrastructure management and automate deployments efficiently. Happy coding!
