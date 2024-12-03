# AWS IAM Management Script
## Overview
This project is part of a capstone assignment for a Linux Administration and Shell Scripting course. It automates the management of AWS Identity and Access Management (IAM) resources using a Bash shell script. The script simplifies the creation of IAM users, groups, and permissions assignment, making it ideal for onboarding new hires in a DevOps environment.

## Features
- Automated IAM User Creation: Create multiple IAM users from a predefined list.
- Group Management: Automatically create an admin group.
- Policy Attachment: Attach the AWS-managed AdministratorAccess policy to the admin group.
- User-Group Assignment: Add IAM users to the admin group for centralized permissions management.
- Error Handling: Includes safeguards to ensure all AWS CLI commands execute successfully.


## Prerequisites
Before running the script, ensure the following:

### 1. AWS CLI:
    - Install the AWS CLI. Installation Guide
    - Configure the CLI using:

    ```bash
    aws configure
    ```
    
    - Provide an Access Key ID and Secret Access Key with sufficient IAM permissions:
        - iam:CreateUser
        - iam:CreateGroup
        - iam:AttachGroupPolicy
        - iam:AddUserToGroup
        
### 2. Bash Shell:
- Ensure you are running the script in a Linux environment with Bash.

### IAM Role Permissions:
- The IAM role or user executing this script must have permissions to manage IAM resources in the AWS account.


## Script Workflow
The script executes the following operations step-by-step:

### 1. Initialization:
    - Loads an array of IAM usernames for iteration.
    - Ensures that the AWS CLI is properly installed and credentials are configured.

### 2. Create IAM Users:
    - Iterates over the array of usernames.
    - Uses the AWS CLI to create each IAM user.

### 3. Create IAM Group:
    - Creates a new IAM group named admin.

### 4. Attach Policy to Group:
- Attaches the AdministratorAccess policy to the admin group, granting full administrative privileges.

### 5. Assign Users to Group:
- Iterates over the IAM usernames.
- Adds each user to the admin group.

### 6. Error Handling:
- Automatically exits the script if any command fails.
- Logs error messages for easy debugging.


## Usage
### 1. Download the Script: Clone this repository to your local machine:
    ```bash
    git clone https://github.com/Danny-Flames/aws-iam-management
    cd aws-iam-management
    ```

### 2. Make the Script Executable:

    ```bash
    chmod +x aws_cloud_manager.sh
    ```

### 3. Run the Script: Execute the script using:

    ```bash
    ./aws_cloud_manager.sh
    ```

### 4. Verify Results:
    - Check created users:

    ```bash
        aws iam list-users
    ```

    - Check the admin group:

    ```bash
    aws iam get-group --group-name admin
    ```

    - Verify attached policies:

    ```bash
    aws iam list-attached-group-policies --group-name admin
    ``` 


## Script Breakdown
### 1. Array Definition
    ```bash
    IAM_USERS=("devops_user1" "devops_user2" "devops_user3" "devops_user4" "devops_user5")
    ```

    - Stores the list of IAM usernames for iteration.

### Function Definitions
#### 1. create_iam_users:
Iterates through the array of usernames and creates an IAM user for each.

#### 2. create_iam_group:
Creates the admin group if it doesn't already exist.

#### 3. attach_admin_policy:
Attaches the AdministratorAccess policy to the admin group.

#### 4. assign_users_to_group:
Assigns all users in the array to the admin group.

#### 5. check_aws_credentials:
Validates that the AWS CLI is configured with credentials.

## Example Output
### Script Execution

    ```bash
        Starting AWS IAM management script...
        Starting IAM user creation process...
        Creating IAM user: devops_user1
        User devops_user1 created successfully.
        Creating IAM user: devops_user2
        User devops_user2 created successfully.
        ...
        Creating IAM group: admin
        Group 'admin' created successfully.
        Attaching AdministratorAccess policy to the 'admin' group...
        AdministratorAccess policy attached to 'admin' group successfully.
        Adding IAM users to the 'admin' group...
        User devops_user1 added to 'admin' group.
        ...
        AWS IAM management completed successfully.
    ```

### Verification
#### Check IAM Users

    ```bash
    aws iam list-users
    ```

#### Output:
    ```bash
    {
        "Users": [
            { "UserName": "devops_user1" },
            { "UserName": "devops_user2" },
            ...
        ]
    }
    ```

#### Check IAM Group

    ```bash
    aws iam get-group --group-name admin
    ```

#### Output:

    ```bash
    {
        "GroupName": "admin",
        "Users": [
            { "UserName": "devops_user1" },
            { "UserName": "devops_user2" },
            ...
        ]
    }
    ```

## Key Learnings
- Mastered AWS CLI commands for IAM management.
- Developed modular shell scripts with reusable functions.
- Incorporated error handling to ensure reliability.
- Improved understanding of role-based access control in AWS.