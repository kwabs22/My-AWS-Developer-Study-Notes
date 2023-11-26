# My-AWS-Developer-Study-Notes

AWS Dev Exam Guide Based Study Notes - Mainly Links, Prompts and CLI focused

November 2023

Developer Associate and DevOps Professional Exam Guides, Whitepapers and Free/Paid Resources

[AWS Certified Developer - Associate Certification (amazon.com)](https://aws.amazon.com/certification/certified-developer-associate/)

Exam Guide = Search Terms = 72 K areas and 64 S areas = 136 areas

32 - Domain 1: Development with AWS Services - Design Concepts, Lamda and Data Stores

K = 22 ( 6, 6, 10 ) S = 15 ( 6, 5, 4 )

26 - Domain 2: Security - Authentication and Authorisation, Encryption, Sensitive Data

K = 18 ( 9, 5, 4 ) S = 13 ( 6, 4, 3 )

24 - Domain 3: Deployment - Artifacts (Images / Config / etc) Prep, Testing, Automate Deployment Testing, AWS CICD

K = 18 ( 4, 3, 3, 8 ) S = 21 ( 4, 4, 5, 8 )

18 - Domain 4: Troubleshooting + Optimisation - Root cause analysis, Observability, Optimise Services and features

K = 14 ( 7, 4, 3 ) S = 15 ( 6, 5, 4 )

[AWS Certified DevOps Engineer - Professional Certification | AWS Certification | AWS (amazon.com)](https://aws.amazon.com/certification/certified-devops-engineer-professional/)

Exam Guide = Search Terms = 59 K areas and 70 S Areas - 129 areas

22% - Domain 1: SDLC Automation -  CICD + Automated testing, Build + Manage Artifacts, Deployment Strategies

K = 11 ( 2, 2, 3, 4 ) S = 18 ( 5, 5, 3, 4 )

17% - Domain 2: Configuration Management and IaC - reusable components, Accounts setup, complex task / envi.s

K = 6 ( 3, 1, 2 ) S = 12 ( 4, 4, 4 )

15% - Domain 3: Resilient Cloud Solutions - Highly Available / Scalability + Bus reqs, Automated Recovery RTO RPO

K = 11 ( 4, 4, 3 ) S = 13 ( 5, 5, 3 )

15% - Domain 4: Monitoring and Logging - Collection, Audit and Monitor logs + metrics to ID issues, Auto Event Man.

K = 14 ( 5, 5, 4 ) S = 20 ( 8, 5, 7 )

14% - Domain 5: Incident and Event Response -  Manage sources + Config changes in resp. to event, Troubleshoot

K = 7 ( 2, 2, 3 ) S = 7 ( 2, 3, 2 )

17% - Domain 6: Security and Compliance - ID + Access Man. , Auto sec + Data Prot., Security mon. + Aud Solution

K = 10 ( 4, 3, 3 ) S = 12 ( 4, 4, 4 )

--------

AWS is just a provider so skills in the exam guide can be based on open source

# AWS based Tools - ChatGPT - Steps to Convert

Migrate Source Code: Move your repositories from GitLab to AWS CodeCommit.

Set up CI/CD Pipelines: Use AWS CodePipeline to orchestrate the workflow and AWS CodeBuild for building and testing your code.

Container Orchestration: Decide between ECS and EKS based on your requirements and migrate your Docker container deployment.

Infrastructure Management: Continue using Terraform or switch to CloudFormation for infrastructure provisioning. Use Ansible or AWS Systems Manager for configuration management.

Security and Monitoring: Implement IAM roles and policies, set up your network with Amazon VPC, and configure monitoring with CloudWatch.

# CI CD Core Tools - TechWorld with Nana - 10 Devops Tools you need to know - The Complete Guide

# [10 DevOps Tools you need to know - The Complete Guide - YouTube](https://youtu.be/UMQGyeAnfFE)

Pipeline 

CICD Tool = Jenkins (GitLab, Github Actions, CircleCI) [Pricing | GitLab](https://about.gitlab.com/pricing/)  https://www.jenkins.io/doc/ 

[Jenkins on Azure documentation - Jenkins | Microsoft Learn](https://learn.microsoft.com/en-us/azure/developer/jenkins/) 

Remote Git Repo → Test → Build → Scans → Artifact Repository → Deploy

Deployment Environment = Cloud Platform

Packaging Apps = Docker (Stateless and Ephemeral) - [Pricing | Docker](https://www.docker.com/pricing/) 

Build Image → Store in Registry → Deploy and run

Container Orchestration = Kubernetes = CKAD- [Certified Kubernetes Application Developer (CKAD) Exam](https://training.linuxfoundation.org/certification/certified-kubernetes-application-developer-ckad/#) 

Auto-Healing, Network Layer to make all container look like one network, Autoscheling and Replica count = Scaling

Each Worker Node = One Cluster?

Monitoring + Alerting Network = Prometheus (Kubernetes)

Part of prometheus = Prometheus Server, Alertmanager, Grafana

IaC (Infra State Management) = Pulumi AI / Terraform - [HashiCorp Terraform: Enterprise Pricing, Packages &amp; Features](https://www.hashicorp.com/products/terraform/pricing) (state)

[Terraform on Azure documentation - Articles, samples, references, and resources - Terraform | Microsoft Learn](https://learn.microsoft.com/en-us/azure/developer/terraform/) 

[Terraform on Google Cloud | Beginner&#39;s Guide - YouTube](https://www.youtube.com/playlist?list=PLpZQVidZ65jO_wtOpLv-HmC9uJgTRB8GT) - Terraform on GCP

Exact Configuration Details = Instant (Stateless) Disaster Recovery and Migration

Configuration Management = Ansible - Patching + Updates

Plugins for Code Editor = VSCode

Ansible Scripts, Kubernetes Manifests, Jenkinsfile, Dockerfile, Terraform, Helm Charts, etc. have plugins

Version Control (Collaboration) = Git

Server OS = Linux = Bash Commands/Scripts



# [Kubernetes Roadmap - Complete Step-by-Step Learning Path - YouTube](https://youtu.be/S8eX0MxfnB4) - TechWorld with Nana



# [you need to learn Docker RIGHT NOW!! // Docker Containers 101 - YouTube](https://youtu.be/eGz9DS-aIeY) - Network Chuck
