# Deploying an Auto Scaling Group (ASG) with Load Balancer using CloudFormation

This guide will walk you through deploying an AWS Auto Scaling Group (ASG) with EC2 instances using a CloudFormation template. The EC2 instances will be behind an Application Load Balancer (ALB), and you will be able to access the application using the ALB's public DNS.

## Prerequisites

Before you begin, ensure you have the following:

- **AWS Account** with permissions to deploy CloudFormation stacks.
- **SSH Key Pair** to access the EC2 instances for troubleshooting (optional).

## Steps to Deploy

### Step 1: Log in to AWS Console
- Open your web browser and log in to the [AWS Management Console](https://aws.amazon.com/console/).

### Step 2: Navigate to CloudFormation
- In the AWS Console, search for **CloudFormation** in the top search bar and click on the **CloudFormation** service.

### Step 3: Create a New Stack
1. Click on **Create Stack**.
2. In the **Choose a template** section, select **Upload a template to Amazon S3**.
3. Click **Choose file** and upload your this CloudFormation YAML file (`scalable-app-with-ec2.yaml`).

### Step 4: Configure Stack Details
1. Click **Next**.
2. Provide a **Stack Name** (e.g., `MyScalableApp`).
3. Fill in any required parameters, such as the **KeyName** for SSH access to the EC2 instances.


### Step 5: Review and Create Stack
1. Review the stack details on the **Review** page.
2. Click **Create Stack**.

### Step 6: Monitor Stack Creation
- You can monitor the progress of your stack in the **CloudFormation Dashboard** under the **Events** tab.
- Wait until the status changes to **CREATE_COMPLETE**.

### Step 7: Retrieve Load Balancer DNS
1. Once the stack is successfully created, go to the **EC2** tab of the AWS Console.
2. Find the **Load Balancer** tab, which provides you the public DNS name of the Application Load Balancer.

### Step 8: Test the Application
1. Copy the **LoadBalancerDNSName** and open it in your web browser:
   ```bash
   http://<LoadBalancerDNSName>
