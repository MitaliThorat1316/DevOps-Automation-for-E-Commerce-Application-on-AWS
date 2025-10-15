# DevOps-Automation-for-E-Commerce-Application-on-AWS
This project delivers the full DevOps lifecycle of an open-source e-commerce application (OpenTelemetry Astronomy Shop) by deploying 20+ microservices on AWS, simulating real-world cloud-native infrastructure and release workflows.

# Project Highlights

- Implements secure and scalable cloud access by creating AWS IAM users, generating access keys via AWS CLI, and launching Ubuntu EC2 instances with SSH connectivity.  
- Containerizes microservices using Docker, building and pushing images to Docker Hub for consistent and repeatable deployments.  
- Provisions infrastructure with Terraform (IaC), utilizing an S3 remote backend and DynamoDB for state locking to ensure safe, collaborative management.  
- Orchestrates microservices on Amazon EKS using Kubernetes manifests and Helm charts, with services and deployments configured for high availability and scalability.  
- Sets up a custom VPC during EKS cluster creation, defining subnets, route tables, and security groups to provide isolated and secure networking.  
- Manages external traffic routing through an ALB Ingress Controller and custom domain integration via GoDaddy and Route 53 for production-grade accessibility.  
- Automates end-to-end CI/CD pipelines with GitHub Actions and Argo CD, enabling GitOps-based delivery to accelerate deployments and reduce manual effort.  

# Project Techstack

- Cloud platform - AWS
- AWS services - AWS IAM users, AWS CLI, EC2 instance, S3, DyanamoDB, Amazon EKS, VPC, Route 53       
- Containerisation - Docker, Docker Hub
- Infrastracture as code - Terraform
- Container orchestration - Kubernetes
- Traffic routing - ALB Ingress Controller
- Domain integration - GoDaddy
- DNS management - Route 53
- CI - Github Actions
- CD - Argo CD

# Project Implementation

## Installations and Prerequisites

- Create AWS account
    - This is the root user

- Create an IAM user with required permissions
    - In the root user account
    - AWS console -> IAM dashboard -> users -> Create user ->  Name- devops-user -> Provide user access to the AWS Management Console - Allow -> Custom password -> Users must create a new password at next sign-in - don't allow 
- Create an EC2 instance
    - In the IAM user account
    - AWS console -> EC2 dashboard -> Launch instance -> Name - devops-demo -> AMI - Ubuntu -> Instance type - t2.large -> Create new key pair - RSA, .pem -> Network settings - auto-assign public IP(enabled), Allow SSH traffic
- Install Docker
- Install Kubectl
- Install Terraform

## Containerization of the project

## Infrastructure as code using Terraform

## Deploying Project to Kubernetes

## Custom Domain configuration for the project

## CI/CD

# Socials

- LinkedIn - https://linkedin.com/in/mitali1609
