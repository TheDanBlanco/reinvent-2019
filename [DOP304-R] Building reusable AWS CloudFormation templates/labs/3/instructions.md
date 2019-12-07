# Lab 3: Modularizing Your Template

## Lab Duration

20 minutes

## Overview

Leading up to this lab, we covered the following concepts in the workshop:

* Import Value
* Splitting existing stacks

This lab will provide hands on experience with the above concepts. You'll be inspecting an existing template and applying some of the best practices you learned.

We're almost there! Our last task is to split our template into multiple templates and reference the values between each other.

## Objective

1. Split up our stacks by lifecycle
2. Reference output values via !ImportValue

## Tasks

### Getting Started:

#### Retrieve the Lab 3 assets

* Retrieve the provided template [here](https://s3.amazonaws.com/ee-assets-prod-us-east-1/modules/c9e293c133bd4b49931316dfaa0f01ad/v1/application-template.yml)

#### Task 1: Split up different stacks by lifecycle

For this task, you'll be creating more templates. You should aim to split up your stacks by lifecycle, considering how often a resource needs to change and how much blast radius you're asking for.

Be sure to include a relevent output for the resources that you're including your new template if they have to be exported.

We'll provide suggestions here on how to split up your stacks but they're by no means hard and fast. 

Stack 1: Processing server security resources:
* IAM Role

Stack 2: Processing server long-lived resources:
* SQS Queue
* S3 Bucket
* SNS Topic

Stack 3: Processing server compute resources:
* EC2 Instance
* Lambda Instance

Stack 4: Processing server alarms & dashboards:
* CloudWatch Alarm
* CloudWatch Anamoly Detector

Stack 5: Default application long-lived resources:
* DynamoDB Table

Stack 6: Default application compute resources:
* EC2 Instance
* EC2 Instance

**Resources**:  
[https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-stack-exports.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-stack-exports.html)

#### Task 2: Import values

For this task, we'll be connecting our stacks together using the `!ImportValue` function. Be sure you export the value from stack A before you import it in stack B.

Here's an example:

```
# template 1
Resources:
  MyIAMRole:
    Type: AWS::IAM::Role
    Properties:
      ...
Outputs:
  MyIAMRole:
    Value: !GetAtt MyIAMRole.Arn
    Export:
      Name: MyIAMRoleArn

# template 2
Resources:
  MyLambda:
    Type: AWS::Lambda::Function
    Properties:
      Role: !ImportValue MyIAMRoleArn
```

**Resources**:  
[https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-importvalue.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-importvalue.html)  

#### Task 3: Deploy your templates!

For this task, we'll be deploying the fruits of our labor. Be sure to deploy your stacks in the correct order to ensure that your resources are available to be exported/imported.

Just as a refresher on how to deploy your templates using the console:

1. In your browser, visit the [CloudFormation Console](https://us-west-2.console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks).
2. Click **Create Stack** and select **with new resources (standard)** in the drop-down.
3. With **Template is ready** selected, click the **Upload a template file** button.
4. Select the provided template file and click **Next**
5. Enter a stack name (i.e. processing-server-compute), fill out any parameters if needed, and click **Next**
6. Scroll down and click **Next**
7. Scroll down and click **Create Stack**

### Going Further

If you've gotten this far, you'll want to look into SSM Parameter Store to store values from CloudFormation exports. This allows you to be a little more flexible when handling imports/exports, such as when editing values, or removing stacks that have imports/exports easily. If you have time, feel free to change your imports/exports to SSM Parameter Store values.

Another important thing to note: CloudFormation will provide a random name to a resource if it's not provided. Unless you need to know the resource name, it's always better to let CloudFormation generate the name to avoid conflicts. Try removing all of your named resources and let CloudFormation generate everything for you.

**Resources**:  
[https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-parameter-store.html](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-parameter-store.html)  
[https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/dynamic-references.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/dynamic-references.html)  

## Running into troubles?

Lab assistants are available if you get stuck at any point during the lab.