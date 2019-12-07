# Lab 1: Template Anatomy

## Lab Duration

20 minutes

## Overview

Leading up to this lab, we covered the following concepts in the workshop:

* Descriptions
* Metadata
* Parameters
* Mappings
* Conditions
* Resources
* Outputs

This lab will provide hands on experience with the above concepts. You'll be inspecting an existing template and applying some of the best practices you learned.

This starting template is a monolithic template with loads of issues - limited sharability, no modularity, hard-coded values - and our task is to fix them! Each lab we'll refactor the template bit by bit. In this lab, we'll focus on removing hard-coded values and improve shareability.

## Objective

1. Move editable values to the parameters section.
2. Add an outputs section.
3. Create a mappings section for logging levels
4. Extra Credit: Set up Groups/Labels/Constraints on parameters

## Tasks

### Getting Started:

#### Retrieve the Lab 1 assets

* Retrieve the provided template [here](https://s3.amazonaws.com/ee-assets-prod-us-east-1/modules/4f72338021624235bb4652243e03a8c0/v1/application-template.yml)

#### Task 1: Deploy the provided application-template.yml template

1. In your browser, visit the [CloudFormation Console](https://us-west-2.console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks).
2. Click **Create Stack** and select **with new resources (standard)** in the drop-down.
3. With **Template is ready** selected, click the **Upload a template file** button.
4. Select the provided **application-template.yml** file and click **Next**
5. Enter a stack name.
6. Scroll down and click **Next**
7. Scroll down, click the "I acknowledge that AWS CloudFormation might create IAM resources with custom names." checkbox, and click **Create Stack**

The stack should deploy in a few minutes.

#### Task 2: Parameterize hardcoded values

For this task, you'll have to examine the **application-template.yml** file and find values that repeat themselves or require a provided hardcoded value to work Don't worry about referencing these values for now, we'll learn that in the next lab. 

1. Create a Parameters section
2. Add parameters for repeated or hardcoded values.
3. Add a parameter called "Environment" with allowed values of "dev", "staging", and "prod"

Hardcoded values:
* ImageId
* my-application-

**Resources**:  
[https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/parameters-section-structure.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/parameters-section-structure.html)  

#### Task 3: Create an outputs section

For this task, we'll want to create an outputs section to get a couple of values for sharing resource between templates later. Don't worry about filling out the "Value" section, we'll fill those out later. The following resources should be exported

* SQS
* DynamoDBTable
* IAMLambdaRole
* SNSTopic

**Resources**:  
[https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/outputs-section-structure.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/outputs-section-structure.html)

#### Task 4: Create a mappings section

For this task, we're going to create a mappings section to choose our logging level based on our environment. We created an "environment" parameter above so we'll be using a mapping section to map that parameter to a value we'll use later.

1. Create a Mappings section
2. Create an EnvironmentVariables mapping
3. Use the log levels we used in the parameters section (dev, staging, prod) as keys
4. Have a LogLevel value of "debug" for dev, "info" for staging, and "error" for prod

**Resources**:  
[https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/mappings-section-structure.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/mappings-section-structure.html)

### Going Further

If you've completed this far, there's more to the parameters/metadata sections compared to what was covered in the workshop. Remember, if you attempt this section you're mostly on your own!

See if you can group, label, and constrain your parameters using the provided documentation.

**Resources:**  
[Parameter Groups](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-cloudformation-interface.html)  
[Parameter Labels](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-cloudformation-interface-parameterlabel.html)  
[Contraints & Allowed Values](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/parameters-section-structure.html)  

## Running into troubles?

Lab assistants are available if you get stuck at any point during the lab.