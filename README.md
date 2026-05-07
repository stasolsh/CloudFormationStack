# AWS CloudFormation Infrastructure Templates

> Practical AWS CloudFormation examples for building scalable, production-style cloud infrastructure.

This repository contains Infrastructure-as-Code templates written in AWS CloudFormation JSON format. The project demonstrates how to provision networking, load balancing, auto scaling, EC2 infrastructure, IAM roles, and deployment protection policies in AWS.

The templates showcase common cloud architecture patterns used in scalable and highly available backend systems.

---

# Project Goals

This repository was created to:

- practice AWS CloudFormation
- understand Infrastructure-as-Code concepts
- learn scalable AWS infrastructure design
- demonstrate reusable cloud architecture patterns
- explore automation and deployment strategies
- strengthen cloud-native and DevOps engineering skills

---

# Technologies Used

- AWS CloudFormation
- AWS EC2
- AWS Auto Scaling
- AWS Application Load Balancer
- AWS IAM
- AWS VPC
- AWS Security Groups
- AWS CloudWatch
- AWS Systems Manager (SSM)

---

# Infrastructure Overview

The project provisions:

- custom VPC
- public subnets
- internet gateway
- route tables
- application load balancer
- launch templates
- auto scaling group
- EC2 instances
- IAM roles and instance profiles
- security groups
- stack protection policies

---

# Architecture Overview

```text
Internet
   ↓
Application Load Balancer
   ↓
Auto Scaling Group
   ↓
EC2 Web Servers
   ↓
VPC + Public Subnets
```

---

# Repository Structure

| File | Description |
|---|---|
| [network-stack.json](network-stack.json) | Creates networking infrastructure including VPC, subnets, route tables, and internet gateway |
| [web-stack.json](web-stack.json) | Deploys scalable web infrastructure with Auto Scaling Group, Launch Template, Application Load Balancer, IAM roles, and security groups |
| [stackpolicy.json](stackpolicy.json) | Defines CloudFormation stack protection policy preventing accidental VPC replacement |

---

# Template Details

## Network Stack

The network template creates:

- VPC with DNS support enabled
- two public subnets
- internet gateway
- public route table
- subnet associations
- VPC outputs for cross-stack usage

Key concepts demonstrated:

- VPC networking
- subnet configuration
- internet access routing
- CloudFormation outputs
- reusable stack composition

---

## Web Stack

The web infrastructure template provisions:

- nested CloudFormation stack
- Application Load Balancer (ALB)
- target groups and listeners
- EC2 launch templates
- Auto Scaling Group
- IAM role and instance profile
- security groups
- rolling deployment policies
- bootstrap automation

Key concepts demonstrated:

- scalable infrastructure
- load balancing
- rolling deployments
- infrastructure automation
- launch templates
- nested stacks
- immutable infrastructure patterns

---

## Stack Policy

The stack policy protects critical resources from accidental replacement during updates.

Protected resource:

- VPC

Key concepts:

- infrastructure protection
- safe deployments
- production safeguards

---

# Features Demonstrated

## High Availability

- multi-subnet deployment
- load balancing
- auto scaling

## Infrastructure Automation

- bootstrap scripts
- launch templates
- nested stacks
- automated provisioning

## Security

- IAM roles
- security groups
- controlled SSH access
- stack protection policy

## Scalability

- Auto Scaling Group
- configurable instance capacity
- load balancing support

---

# Getting Started

## Prerequisites

- AWS account
- AWS CLI configured
- CloudFormation permissions
- EC2 key pair

---

# Deploy Network Stack

```bash
aws cloudformation create-stack \
  --stack-name network-stack \
  --template-body file://network-stack.json
```

---

# Deploy Web Stack

```bash
aws cloudformation create-stack \
  --stack-name web-stack \
  --template-body file://web-stack.json \
  --capabilities CAPABILITY_NAMED_IAM \
  --parameters ParameterKey=KeyName,ParameterValue=my-key
```

---

# Apply Stack Policy

```bash
aws cloudformation set-stack-policy \
  --stack-name network-stack \
  --stack-policy-body file://stackpolicy.json
```