## Creating an AWS CodeBuild Service Role via AWS CLI
Here's how to create an IAM role for AWS CodeBuild with the necessary permissions using AWS CLI commands:

## 1. Create a Trust Policy File
First, create a file named codebuild-trust-policy.json with the following content:

json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "codebuild.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
## 2. Create the IAM Role
Run this command to create the role:

bash
aws iam create-role \
  --role-name CodeBuildServiceRole \
  --assume-role-policy-document file://codebuild-trust-policy.json
## 3. Create a Permissions Policy File
Create a file named codebuild-policy.json with these permissions (customize as needed):

json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Resource": [
        "*"
      ],
      "Action": [
        "logs:CreateLogGroup",
        "logs:CreateLogStream",
        "logs:PutLogEvents",
        "s3:GetObject",
        "s3:GetObjectVersion",
        "s3:PutObject",
        "s3:GetBucketAcl",
        "s3:GetBucketLocation",
        "codecommit:GitPull",
        "ecr:BatchCheckLayerAvailability",
        "ecr:CompleteLayerUpload",
        "ecr:GetAuthorizationToken",
        "ecr:InitiateLayerUpload",
        "ecr:PutImage",
        "ecr:UploadLayerPart"
      ]
    }
  ]
}
## 4. Attach the Permissions Policy to the Role
bash
aws iam put-role-policy \
  --role-name CodeBuildServiceRole \
  --policy-name CodeBuildServicePolicy \
  --policy-document file://codebuild-policy.json
## 5. Attach the AWS Managed CodeBuild Policy (Optional)
For additional permissions, you can attach the AWS managed policy:

bash
aws iam attach-role-policy \
  --role-name CodeBuildServiceRole \
  --policy-arn arn:aws:iam::aws:policy/AWSCodeBuildAdminAccess
## 6. Get the Role ARN
To get the ARN of your newly created role (needed for CodeBuild project creation):

bash
aws iam get-role --role-name CodeBuildServiceRole --query 'Role.Arn' --output text
