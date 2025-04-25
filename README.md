# aws-codebuild
# AWS CodeBuild Python Hello World Lab

This lab demonstrates how to set up a continuous integration pipeline for a Python application using AWS CodeBuild.

## Overview

The project includes:
- A simple Python "Hello World" script
- A build specification file for AWS CodeBuild
- AWS CLI commands to create and manage the CodeBuild project

## Prerequisites

- AWS account with appropriate permissions
- AWS CLI installed and configured
- Git repository (CodeCommit, GitHub, etc.) to store the code
- IAM role for CodeBuild with necessary permissions

## Project Structure
├── hello.py # Python Hello World script
├── buildspec.yml # CodeBuild build specification
└── README.md # This documentation


## Python Application

The `hello.py` file contains a simple Python script that prints a greeting and performs a basic calculation:

```python
#!/usr/bin/env python3

def main():
    print("Hello, AWS CodeBuild World!")
    
    # Demonstrate a simple calculation
    x = 5
    y = 7
    print(f"{x} + {y} = {x + y}")

if __name__ == "__main__":
    main()

## Build Specification
The buildspec.yml file defines the build process:

Install phase: Sets up Python 3.9 runtime and installs dependencies

Pre-build phase: Verifies Python and pip versions

Build phase: Executes the Python script

Post-build phase: Records completion timestamp

## Customization Options
Python Version: Update the runtime version in buildspec.yml

Dependencies: Add a requirements.txt file and uncomment the pip install line

Artifacts: Modify the artifacts section in buildspec.yml to store build outputs

Notifications: Configure SNS notifications for build events

## Expected Output
When the build runs successfully, you should see output similar to:
[Container] Running command: python hello.py
Hello, AWS CodeBuild World!
5 + 7 = 12
