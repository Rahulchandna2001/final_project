# final_project

# AWS Infrastructure Automation with Terraform

This project automates the deployment of AWS infrastructure using Terraform, implementing best practices for Infrastructure as Code (IaC). The resources include an S3 bucket for state management, a DynamoDB table for state locking, a VPC with public subnet, and an EC2 instance with a security group.

# Features

1. S3 Bucket and State Management**
   - S3 bucket (`rahul-bucket-terraform`) is created to store the Terraform state file.
   - Versioning is enabled to track changes over time.
   - DynamoDB table (`rahul-lock-table-terraform`) is configured for state locking to prevent concurrent updates.

2. Custom VPC and EC2 Instance
   - A VPC (`10.0.0.0/16`) with a public subnet (`10.0.1.0/24`) is defined.
   - Internet Gateway and route tables are configured for internet access.
   - An EC2 instance is provisioned with the following:
     - AMI: `ami-0453ec754f44f9a4a`
     - Instance type: `t2.micro`
     - Security group allowing:
       - SSH access on port 22.
       - HTTP traffic on port 80.

3. Terraform Backend Configuration
   - Terraform is configured to use the S3 bucket for backend state management.
   - State locking is enabled via the DynamoDB table.

4. Variables and Modularization
   - Variables are defined in `variables.tf` for modularity and reusability.
   - Specific values are stored in `vars.tfvars`, keeping sensitive data separate from the codebase.

# Files in the Repository

- `provider.tf`: Configures the AWS provider.
- `s3_bucket.tf`: Creates the S3 bucket and enables versioning.
- `dynamodb.tf`: Sets up the DynamoDB table for state locking.
- `network.tf`: Defines the VPC, subnet, Internet Gateway, and route table.
- `ec2.tf`: Configures the EC2 instance and its security group.
- `variable.tf`: Defines variables for reusability.
- `vars.tfvars`: Stores actual values for the variables.

# Steps to Deploy the Infrastructure

1. Initialize Terraform
   ```bash
   terraform init
   ```

2. Plan the Deployment
   ```bash
   terraform plan
   ```

3. Apply the Configuration
   ```bash
   terraform apply
   ```

4. Verify Resources
   - Check the AWS Management Console to confirm:
     - The S3 bucket and state file.
     - The DynamoDB table for state locking.
     - The running EC2 instance with the specified configuration.
     - The VPC and subnet.

# Key Configuration Details

- S3 Bucket
  - Name: `rahul-bucket-terraform`
  - Versioning: Enabled

- DynamoDB Table
  - Name: `rahul-lock-table-terraform`

- VPC and Subnet
  - VPC CIDR: `10.0.0.0/16`
  - Subnet CIDR: `10.0.1.0/24`

- EC2 Instance
  - AMI: `ami-0453ec754f44f9a4a`
  - Instance type: `t2.micro`

# Screenshots

- Running EC2 instance in AWS Management Console.
- Terraform apply output showing resource creation.
- S3 bucket displaying the `tfstate` file.
- DynamoDB table showing state locking entries.

# Challenges and Best Practices

- Modularized code for reusability and maintainability.
- Sensitive data (e.g., AWS credentials) is excluded from version control.
- Followed best practices for backend configuration and state management.


