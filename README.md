# 🚀 Amazon EKS Cluster Setup using eksctl

This guide walks you through setting up an **EKS Cluster** on AWS step by step using `eksctl`, `kubectl`, and AWS CLI.

---

## Step 1: Create EKS Management Host in AWS
1. Launch a new **Ubuntu VM** in AWS EC2 (`t2.micro` is fine for management).
2. Connect to the machine via SSH.
3. Install **kubectl**:
   ```bash
   curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.19.6/2021-01-05/bin/linux/amd64/kubectl
   chmod +x ./kubectl
   sudo mv ./kubectl /usr/local/bin
   kubectl version --short --client

4. Install AWS CLI latest version using below commands
    ```bash
    sudo apt install unzip
    curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
    unzip awscliv2.zip
    sudo ./aws/install
    aws --version

5. Install EKSctl 
     ```bash
   curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
   sudo mv /tmp/eksctl /usr/local/bin
   eksctl version

## Step 3:Create IAM role & attach to EKS Management Host

1. Create New Role using IAM service ( Select Usecase - ec2 )
2. Add below permissions for the role
  Administrator - acces
3. Enter Role Name (eksroleec2)

4. Attach created role to EKS Management Host (Select EC2 => Click on Security => Modify IAM Role => attach IAM role we have created)


 
## Step 4:Create EKS Cluster using eksctl
 ```bash
eksctl create cluster \
  --name ekscluster \
  --version 1.30 \
  --region ap-south-1 \
  --nodegroup-name linux-node \
  --node-type t2.micro \
  --nodes 2

 
## After few mins we will be able to see cluster live.

After use delete the cluster other wise it will geenrate huge bills.
command to delete :- 
 ```bash
eksctl delete cluster --name ashokit-cluster4 --region ap-south-1