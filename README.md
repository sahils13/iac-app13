GitOps-Based Cloud Deployment on AWS EKS
A production-style GitOps pipeline that provisions AWS infrastructure using Terraform and deploys a Java web application to Kubernetes — fully automated through GitHub Actions.
---
Architecture Overview
```
Developer Push
      │
      ▼
GitHub Actions CI/CD
      │
      ├── Build & Test (Maven)
      ├── Docker Build & Push (ECR)
      ├── Terraform: Provision VPC + EKS
      └── Deploy to EKS via Helm + Ansible
```
---
Tech Stack
Layer	Tools
Infrastructure (IaC)	Terraform
Cloud	AWS EKS, VPC, IAM, ECR
CI/CD	GitHub Actions
Containerization	Docker
Deployment	Helm, Kubernetes, Ansible
Application	Java (Spring MVC, Spring Security, MySQL)
---
Repositories
This project is split across two repos:
iac-app13 — Terraform code to provision AWS VPC + EKS cluster
app13-action — Application code with GitHub Actions pipeline, Helm charts, Kubernetes manifests, Ansible playbooks
---
What This Project Does
Infrastructure provisioned via Terraform — VPC, subnets, IAM roles, and EKS cluster created and version-controlled. Any infra change goes through Git.
CI/CD via GitHub Actions — On every push, the pipeline builds the Java app using Maven, runs tests, builds a Docker image, and pushes to container registry.
Deployment via Helm + Ansible — Application is deployed to the EKS cluster using Helm charts. Ansible handles configuration and environment setup.
Everything managed through Git — No manual deployments. Infrastructure and application state both tracked in version control.
---
How to Run
Prerequisites
AWS CLI configured
Terraform v1.6.3+
kubectl
Helm 3+
Step 1 — Provision Infrastructure
```bash
cd terraform/
terraform init
terraform validate
terraform plan -out planfile
terraform apply -auto-approve -input=false planfile
```
Step 2 — Configure kubectl
```bash
aws eks update-kubeconfig --name <cluster-name> --region <region>
```
Step 3 — Deploy Application
Push to main branch — GitHub Actions pipeline handles the rest automatically.
---
Key Learnings
Managing AWS infrastructure as code using Terraform with remote state
Setting up EKS cluster with proper VPC, subnet, and IAM configuration
Building end-to-end CI/CD pipeline using GitHub Actions
Deploying containerized applications to Kubernetes using Helm
Using Ansible for configuration management in a cloud environment
---
Author
Sahil Sonkar — GitHub | LinkedIn
