# aws-infra
Deploy AWS infra via terraform using Azure DevOps

# Terraform Azure DevOps Pipeline

## Overview
This Azure DevOps pipeline automates Terraform deployment and destruction processes with manual approvals at key stages. It includes build, approval, deployment, and destruction stages to manage infrastructure efficiently.

## Pipeline Structure

### 1. Build Stage
**Purpose**: Initializes Terraform and creates an execution plan.
- Installs Terraform
- Initializes Terraform backend in AWS S3
- Runs `terraform plan` to generate an execution plan

### 2. Manual Approval Before Deployment
**Purpose**: Requires manual review and approval before proceeding with deployment.
- Notifies `ravtflab@gmail.com`
- Requires user approval before executing Terraform Apply

### 3. Deploy Stage
**Purpose**: Deploys the Terraform infrastructure.
- Reinitializes Terraform backend
- Executes `terraform apply` to provision resources

### 4. Manual Approval Before Destroy
**Purpose**: Requires manual confirmation before destroying resources.
- Notifies `ravitflab@gmail.com`
- Ensures resources are reviewed before teardown

### 5. Destroy Stage
**Purpose**: Destroys the deployed infrastructure.
- Reinitializes Terraform backend
- Runs `terraform destroy` to remove resources

## Backend Configuration
The pipeline uses AWS S3 and DynamoDB for state management:
- **S3 Bucket**: `terraform-state-1999`
- **State File Key**: `terraform.tfstate`
- **Backend Region**: `aws-us-east-lab`

## Trigger
- **Trigger Mode**: Manual (`none`), meaning it will not run automatically and must be manually triggered in Azure DevOps.

## Usage
1. Trigger the pipeline manually.
2. Review and approve Terraform Plan before deployment.
3. Review and approve Terraform Destroy before teardown.

This setup ensures controlled deployments with approvals at critical stages.


