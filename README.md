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


