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
  - Go to [AWS sign-up page](https://signin.aws.amazon.com/signup?request_type=register)and follow the steps
  - You'll need a debit or credit card
  - This will be your root user account
 
***In the root user account***
    
- Create an IAM user with required permissions
  - AWS console -> IAM dashboard -> users -> Create user ->  Name- devops-user -> Provide user access to the AWS Management Console - Allow -> Custom password ->
    Users    must create a new password at next sign-in - don't allow -> Next -> Set permissions - Attach policies directly -> Permissions policies - AdministratorAccess -> Next -> Create user -> Download .csv file

***In the IAM user account***
      
- Create an EC2 instance
  - Region - London (eu-west-2)
  - AWS console -> EC2 dashboard -> Launch instance -> Name - devops-demo -> AMI - Ubuntu -> Instance type - t2.large -> Create new key pair - devops-demo(name), RSA,
      .pem, create key pair (the devops-demo.pem file will we downloaded on your machine) -> Network settings - auto-assign public IP(enabled), Allow SSH traffic -> Launch Instance
      
- SSH into the EC2 insance
  - Once the Instance state is 'running', click on the Instance and copy the 'Public IPv4 address'
  - Go to your machine's command-line tool (for me it's command prompt)
  - In cmd, go to the folder where devops-demo.pem file in downloaded
  - Run ```ssh -i devops-demo.pem ubuntu@<IPv4 address> ``` , ubuntu is the default username for AWS EC2 with ubuntu AMI
  - If it doesn't work, Run ```chmod 400 devops-demo.pem``` and try again

***In the EC2 instance:***

- Install Docker
  - [Install docker engine](https://docs.docker.com/engine/install/)
  - Go to 'Install using the apt repository section' and follow the steps
  - Or you can follow the below steps:
    ```bash
    # Add Docker's official GPG key:
    sudo apt-get update
    sudo apt-get install ca-certificates curl
    sudo install -m 0755 -d /etc/apt/keyrings
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
    sudo chmod a+r /etc/apt/keyrings/docker.asc
            
    # Add the repository to Apt sources:
    echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
    $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
    sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    sudo apt-get update

    # Install the Docker packages:
    sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

    # Verify that the installation is successful by running the hello-world image:
    sudo docker run hello-world
    ```
  - Use ```sudo docker ps``` to check installation
  - To grant access of docker to Ubuntu use ```sudo usermod -aG docker ubuntu```, then you can directly run ```docker ps```
  
- Install Kubectl
  - [Install kubectl](https://kubernetes.io/docs/tasks/tools/)
  - Go to 'Install kubectl on Linux -> Install kubectl binary with curl on Linux' then follow the steps
  - Or just follow these steps:
    ```bash
    # Download the latest release with the command:
    curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

    # Validate the binary:
    curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"

    # Validate the kubectl binary against the checksum file:
    echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check

    # Install kubectl
    sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl

    # Test to ensure the version you installed is up-to-date:
    kubectl version --client
    ```
- Install Terraform
  - [Install terraform](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)
  - Go to 'Install terraform -> Linux -> Ubuntu/Debian' and follow the steps
  - Or follow these steps:
    ```bash
    # HashiCorp's Debian package repository.
    sudo apt-get update && sudo apt-get install -y gnupg software-properties-common

    # Install HashiCorp's GPG key.
    wget -O- https://apt.releases.hashicorp.com/gpg | \
    gpg --dearmor | \
    sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg > /dev/null

    # Verify the GPG key's fingerprint.
    gpg --no-default-keyring \
    --keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg \
    --fingerprint

    # Add the official HashiCorp repository to your system.
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(grep -oP '(?<=UBUNTU_CODENAME=).*' /etc/os-release || lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list

    # Update apt to download the package information from the HashiCorp repository.
    sudo apt update

    # Install Terraform from the new repository.
    sudo apt-get install terraform

    # Verify the Installation
    terraform -help
    ```

## Containerization of the project

## Infrastructure as code using Terraform

## Deploying Project to Kubernetes

## Custom Domain configuration for the project

## CI/CD

# Socials

- LinkedIn - https://linkedin.com/in/mitali1609
