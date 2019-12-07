# Lab 0: Setting Up Your Editor

## Lab Duration

20 minutes

## Overview

Leading up to this lab, we covered the following concepts in the workshop:

* editors
* cfn-lint

This lab will provide hands on experience with the above concepts. You'll be deploying an existing CloudFormation template to create a Cloud9 environment in your provided AWS account. 

## Objective

1. Create a remote Cloud9 environment.
2. Install cfn-lint on your remote Cloud9 environment.
3. Extra Credit: Install a local IDE and a local version of cfn-lint

## Tasks

### Getting Started:

#### Retrieve the Lab 0 assets

* Retrieve the provided template [here](https://s3.amazonaws.com/ee-assets-prod-us-east-1/modules/5ee8cdaf5ec342fb8e67ccfc2ea0ab46/v1/cloud9-template.yml)

#### Task 1: Deploy the provided cloud9-template.yml template

1. In your browser, visit the [CloudFormation Console](https://us-west-2.console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks).
2. Click **Create Stack** and select **with new resources (standard)** in the drop-down.
3. With **Template is ready** selected, click the **Upload a template file** button.
4. Select the provided **cloud9-template.yml** file and click **Next**
5. Enter a stack name (i.e. cloud9-environment), select the first **SubnetId**, and click **Next**
6. Scroll down and click **Next**
7. Scroll down and click **Create Stack**

The stack should deploy in a few minutes.

#### Task 2: Install cfn-lint in your Cloud9 remote environment

1. In your browser, visit the [Cloud9 Console](https://us-west-2.console.aws.amazon.com/cloud9/home#)
2. Click **Open IDE** on your Cloud9 environment. (Cloud9-(random characters))
3. Type **pip install cfn-lint --user** in the integrated terminal near the bottom of your environment. 
4. Once installed, type **cfn-lint -v**. You should see a version reported back.
5. Use cfn lint by typing **cfn-lint [yourtemplatefile]**.

### Going Further

Try installing your favored IDE locally and setting up [cfn-lint](https://github.com/aws-cloudformation/cfn-python-lint) locally. We won't be able to provide too much support in this task as there are wide variety of customer hardware and security issues that prevent us from helping much further than basic troubleshooting. If you aren't able to install locally, you can always fall back to your Cloud9 environment.

## Running into troubles?

Lab assistants are available if you get stuck at any point during the lab.