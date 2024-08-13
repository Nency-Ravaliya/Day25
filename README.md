# Custom IAM Policy for S3 Access

## Overview

This document outlines the steps to implement a custom IAM policy to grant specific permissions to the "DevTeamRole" IAM role for accessing the S3 bucket named `application-logs`. The policy will allow listing and reading objects from the bucket, with no other actions permitted.

## Steps to Implement the Policy

### 1. Understand the Requirements

- **Bucket Name**: `application-logs`
- **IAM Role**: `DevTeamRole`
- **Permissions Needed**:
  - `s3:ListBucket` – To list objects in the bucket.
  - `s3:GetObject` – To read objects from the bucket.
- **Restrictions**: No other actions (e.g., delete, write) should be allowed.

### 2. Create a New IAM Policy

1. **Navigate to the IAM Console**:
   - Go to the [IAM Management Console](https://console.aws.amazon.com/iam/).

2. **Create a New Policy**:
   - Click on **Policies** in the left-hand menu.
   - Click on **Create policy**.

3. **Define the Policy**:
   - Switch to the **JSON** tab and enter the following policy JSON:

     ```json
     {
         "Version": "2012-10-17",
         "Statement": [
             {
                 "Effect": "Allow",
                 "Action": "s3:ListBucket",
                 "Resource": "arn:aws:s3:::application-logs"
             },
             {
                 "Effect": "Allow",
                 "Action": "s3:GetObject",
                 "Resource": "arn:aws:s3:::application-logs/*"
             }
         ]
     }
     ```

   - Click **Review policy**.

4. **Name and Describe the Policy**:
   - Enter a policy name (e.g., `DevTeamS3AccessPolicy`).
   - Optionally, add a description (e.g., "Policy to allow listing and reading objects from the application-logs bucket").
   - Click **Create policy**.

### 3. Attach the Policy to the IAM Role

1. **Navigate to IAM Roles**:
   - Go to **Roles** in the IAM Management Console.

2. **Select the Role**:
   - Search for and select the `DevTeamRole`.

3. **Attach the Policy**:
   - Click on **Add permissions**.
   - Select **Attach policies**.
   - Search for and select the newly created policy (`DevTeamS3AccessPolicy`).
   - Click **Next: Review**, then **Add permissions**.

### 4. Test the Policy

1. **Access the S3 Bucket**:
   - Assume the `DevTeamRole` using the AWS Management Console or AWS CLI.

2. **Perform Allowed Actions**:
   - **List Objects**: Verify that you can list objects in the `application-logs` bucket.
   - **Read Objects**: Verify that you can read (download) objects from the bucket.

3. **Verify Denied Actions**:
   - Attempt actions outside the allowed scope (e.g., delete or write objects) and confirm that these actions are denied.

### 5. Document the Results

- **Successful Actions**: Document that listing and reading objects from the bucket are successful.
- **Denied Actions**: Document that actions such as deleting or writing objects are correctly denied.

## Conclusion

The custom IAM policy has been implemented to grant the "DevTeamRole" the necessary permissions to list and read objects from the `application-logs` S3 bucket. The policy restricts all other actions to ensure the security and integrity of the bucket's contents.

==================================================

# Multi-Tier Architecture Solution Estimation

## Overview

This document outlines the design and cost estimation process for a scalable web application architecture. The architecture includes an Application Load Balancer, EC2 instances for the application tier, and an RDS instance for the database tier. The solution is designed to support up to 100,000 concurrent users.

## 1. Define the Architecture

### Components Required

1. **Application Load Balancer (ALB)**: Distributes incoming traffic across multiple EC2 instances.
2. **EC2 Instances**: Hosts the application servers to handle user requests.
3. **RDS Instance**: Manages the database for storing and retrieving application data.

### Expected Traffic and Configuration

- **Load Balancer**: Handles incoming traffic and distributes it efficiently.
- **EC2 Instances**: Select instance types based on expected load and application requirements.
- **RDS Instance**: Choose a configuration that supports the expected data workload and performance needs.

## 2. Select AWS Services

### Application Load Balancer

- **Service**: AWS Application Load Balancer
- **Configuration**: Set up to distribute incoming traffic across multiple EC2 instances.

### EC2 Instances

- **Instance Type**: `t3.medium`
  - **vCPUs**: 2
  - **Memory**: 8 GiB
  - **Usage**: Suitable for moderate application workloads and balancing between cost and performance.

### RDS Instance

- **Instance Type**: `db.m5.large`
  - **vCPUs**: 2
  - **Memory**: 8 GiB
  - **Usage**: Provides balanced compute and memory resources for the database tier.

## 3. Estimate Costs Using AWS Pricing Calculator

1. **Navigate to the AWS Pricing Calculator**:
   - Go to the [AWS Pricing Calculator](https://calculator.aws/).

2. **Add Components to the Estimate**:

   - **Application Load Balancer**:
     - Configure the load balancer based on expected traffic.
     - Include cost factors such as number of hours and data processed.

   - **EC2 Instances**:
     - Select `t3.medium` instances.
     - Specify the number of instances required (e.g., 10 instances) and estimate usage hours.
     - Consider additional costs such as EBS storage and data transfer.

   - **RDS Instance**:
     - Choose `db.m5.large` instance.
     - Specify storage requirements and estimated usage hours.
     - Include costs for backups and data transfer.

3. **Configure Service Specifications**:
   - Adjust settings based on expected load and storage requirements.

4. **Review the Estimate**:
   - Review the total estimated monthly cost for all components.

## 4. Document and Analyze the Estimate

### Total Estimated Monthly Cost

- **Load Balancer Cost**: [Specify the cost]
- **EC2 Instances Cost**: [Specify the cost]
- **RDS Instance Cost**: [Specify the cost]
- **Total Estimated Cost**: [Specify the total cost]

### Cost-Saving Measures

- **Reserved Instances**: Consider purchasing reserved instances for EC2 and RDS to save on long-term costs.
- **Auto Scaling**: Implement Auto Scaling for EC2 instances to handle traffic variations and optimize usage.
- **Storage Optimization**: Review storage needs and consider using cost-effective storage options.

## 5. Prepare a Report

### Architecture Design

- **Diagram**: [Include an architecture diagram if available]
- **Components**: Application Load Balancer, EC2 instances, RDS instance

### Cost Estimate

- **Detailed Costs**: Breakdown of costs for each component
- **Total Estimated Monthly Cost**: [Specify the total cost]

### Recommendations

- **Performance**: Ensure adequate resources to handle up to 100,000 concurrent users.
- **Cost Optimization**: Implement reserved instances, Auto Scaling, and storage optimization strategies.
- **Scalability**: Plan for future growth and scalability based on traffic projections and application needs.

## Conclusion

The multi-tier architecture has been designed to support a scalable web application with an estimated cost for the required AWS services. The recommendations provided will help maintain performance while optimizing costs and accommodating future growth.



