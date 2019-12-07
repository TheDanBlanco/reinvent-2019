# Lab 2: Intrinsics & Pseudo Params

## Lab Duration

20 minutes

## Overview

Leading up to this lab, we covered the following concepts in the workshop:

* Intrinsic Functions
  * Base64
  * Select
  * Split
  * Cidr
  * GetAZs
  * Ref
  * GetAtt
  * FindInMap
  * Join
  * Sub
  * Equals
  * If
  * And
  * Or
  * Not
* Psuedo Parameters 
  * AccountId
  * NotificationArns
  * NoValue
  * Partition
  * Region
  * StackId
  * StackName
  * UrlSuffix

This lab will provide hands on experience with the above concepts. You'll be inspecting an existing template and applying some of the best practices you learned.

We've parameterized our template, created a mapping, and added an outputs section. In this lab we'll be wiring our template together, referencing parameters, using a proper mapping, and exporting our output values. We'll also be replacing hardcoded values with pseudo parameters as appropriate. 

## Objective

1. Wire up parameters in our template
2. Reference the values in our mapping as appropriate
3. Use resource values in our outputs section
4. Extra Credit: Convert !Joins to !Sub where appropriate

## Tasks

### Getting Started:

#### Retrieve the Lab 2 assets

* Retrieve the provided template [here](https://s3.amazonaws.com/ee-assets-prod-us-east-1/modules/1f52584e99e741fa9cb296bc0876643f/v1/application-template.yml)

#### Task 1: Wire up your parameters using the !Ref Intrinsic function

For this task, you'll be wiring up the parameters we wrote in the last lab. Anywhere you'd like to reference your parameter, use the `!Ref` intrinsic function. Here's an example:

```
Resource:
  MyResource:
    Type: ...
    Properties:
      MyParameterProperty: !Ref MyParameter
```

**Resources**:  
[https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-ref.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-ref.html)
[https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-anatomy.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-anatomy.html)

#### Task 2: Reference the values in our mapping

For this task, we'll be wiring up the mappings much the same way we did with our parameters. The important intrinsic we'll be using is `!FindInMap`. Our mapping function should be used in our Lambda resource instead of the hardcoded value. Remember to refer to the value of the property to dynamically pull the correct value. Here's an example:

```
Resource:
  MyResource:
    Type: ...
    Properties:
      MyMappingProperty: !FindInMap [ EnvironmentVariables, !Ref Environment, LogLevel ]
```

**Resources**:  
[https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-findinmap.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-findinmap.html)
[https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/parameters-section-structure.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/parameters-section-structure.html)
[https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-anatomy.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-anatomy.html)

#### Task 3: Reference the values in our Outputs section

For this task, we'll be wiring up the outputs in the same way we did with the parameters and mappings. We'll be using both !Ref and !GetAtt functions as appropriate. Remember that Refs and GetAtts refer to the output values of a resource.

Here's a [cheatsheet](https://theburningmonk.com/cloudformation-ref-and-getatt-cheatsheet/) to know what's a Ref and what's a GetAtt  

We want the following values from our resources:

1. SQS Queue Arn
2. DynamoDB Table Arn
3. IAM Lambda Role Arn
4. SNS Topic Arn

```
  SQSProcessing:
    Description: SQS export
    Value: !GetAtt SQSProcessing.Arn
    Export:
      Name: SQSProcessingQueue
```

**Resources**:  
[https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-ref.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-ref.html)  
[https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-getatt.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-getatt.html)  
[https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-anatomy.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-anatomy.html)

### Going Further

If you've gotten this far, there are a couple of things you can do to further improve the template. 

First, reference the values exported by the resource throughout the template. For example, manually building ARNs by Joins or Subs when they can get referenced with a Ref or a GetAtt isn't a best practice. Remember: Subs and GetAtts create an implicit dependency, so we can remove any DependsOn we find.

Second, lets try to replace any remaining Joins with Refs where appropriate. Remember, Subs are almost always easier to read, write, and reason about.

Finally, you can future proof your Image Ids by having CloudFormation look up the latest values instead of having to manually change them every time.

**Resources**:  
[https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-ref.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-ref.html)  
[https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-getatt.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-getatt.html)  
[https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-sub.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-sub.html)  
[Finding the latest Image Ids using Parameter Store and CloudFormation](https://aws.amazon.com/blogs/compute/query-for-the-latest-amazon-linux-ami-ids-using-aws-systems-manager-parameter-store/)  

## Running into troubles?

Lab assistants are available if you get stuck at any point during the lab.