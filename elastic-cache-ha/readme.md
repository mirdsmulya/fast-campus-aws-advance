## Steps to Deploy ElastiCache using CloudFormation

### Step 1: Prepare the Template
- **Copy and Save**: Copy the provided YAML template into a text editor (e.g., Notepad, VS Code) and save it as `elasticache-ha-deployment.yaml`.

### Step 2: Log in to AWS Console
- **Access AWS Console**: Open [AWS Management Console](https://aws.amazon.com/console/).
- **Login**: Enter your credentials.

### Step 3: Navigate to CloudFormation
- **Open CloudFormation**: Search for "CloudFormation" in the AWS Console and select it.
- **Create Stack**: Click **Create stack** and select **With new resources (standard)**.

### Step 4: Upload the Template
- **Choose Template**: Under **Specify template**, select **Upload a template file**.
- **Upload File**: Upload the `elasticache-ha-deployment.yaml` file.
- **Proceed**: Click **Next**.

### Step 5: Configure Stack Details
- **Name the Stack**: Enter a stack name (e.g., `ElastiCacheHAStack`).
- **Specify Parameters**:
  - **VPC**: Select your VPC ID.
  - **SubnetA**: Choose a subnet ID.
  - **SubnetB**: Choose another subnet ID.
  - **SubnetC**: Choose a third subnet ID.
- **Proceed**: Click **Next**.

### Step 6: Configure Stack Options
- **Proceed**: Click **Next**.

### Step 7: Review and Deploy
- **Review**: Ensure all details are correct.
- **Deploy**: Click **Create stack**.

### Step 8: Monitor Deployment
- **Check Status**: Watch the stack status in CloudFormation until it shows **CREATE_COMPLETE**.

### Step 9: Verify Deployment
- **ElastiCache Dashboard**: Go to the ElastiCache service, select Redis, and ensure the replication group spans multiple availability zones.
- **Test Connectivity**: Use the primary endpoint from CloudFormation outputs to connect to your Redis cluster.

### Step 10: Clean Up (Optional)
- **Delete the Stack**: To remove all resources, delete the stack from the CloudFormation dashboard.

By following these steps, you'll deploy a highly available ElastiCache cluster using AWS CloudFormation.
