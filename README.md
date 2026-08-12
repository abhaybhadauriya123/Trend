Trend – AWS DevOps CI/CD Deployment

Project Overview

Trend is a production-ready web application deployed on AWS using Docker, Amazon ECR, Amazon EKS, Kubernetes, AWS CodeBuild, AWS CodePipeline, and a Kubernetes LoadBalancer.

The objective of this project is to demonstrate an end-to-end CI/CD deployment workflow from GitHub to a running application on Amazon EKS.

GitHub Repository

https://github.com/abhaybhadauriya123/Trend

Architecture

GitHub Repository→ AWS CodePipeline→ AWS CodeBuild→ Docker Image / Amazon ECR→ Amazon EKS (trend-cluster)→ Kubernetes Deployment→ Kubernetes Service (trend-app-service)→ AWS Load Balancer→ Trend Application

AWS Resources

Resource

Value

AWS Region

ap-south-1 (Asia Pacific – Mumbai)

GitHub Repository

abhaybhadauriya123/Trend

CodeBuild Project

trend-codebuild-role

CodePipeline

trend-pipeline

EKS Cluster

trend-cluster

Kubernetes Deployment

trend-app

Kubernetes Service

trend-app-service

Service Type

LoadBalancer

Application Port

3000

Load Balancer DNS

a2f548479cd504fb4b5b3b1e1aad253b-1757595433.ap-south-1.elb.amazonaws.com

Load Balancer ARN

arn:aws:elasticloadbalancing:ap-south-1:080641083688:loadbalancer/a2f548479cd504fb4b5b3b1e1aad253b

Application URL

http://a2f548479cd504fb4b5b3b1e1aad253b-1757595433.ap-south-1.elb.amazonaws.com:3000

CI/CD Pipeline

1. Source Stage

GitHub is configured as the source provider through an AWS-managed GitHub App connection.

Repository:abhaybhadauriya123/Trend

Branch:main

2. Build Stage

AWS CodeBuild project:trend-codebuild-role

The build process uses the repository build configuration and prepares the application/container deployment artifacts.

3. Deploy Stage

AWS CodePipeline deploys to Amazon EKS.

EKS cluster:trend-cluster

Kubernetes manifest:deployment.yaml

The deployment was successfully completed after configuring the CodePipeline service role as an EKS access entry.

Kubernetes Validation

The deployment was verified from the Ubuntu AWS EC2 environment.

Expected/verified commands:

kubectl get pods -A
kubectl get deployments -A
kubectl get services -A

The application pods were running with 1/1 Running, the deployment showed 2/2 available, and the service was exposed through a Kubernetes LoadBalancer.

Application Access

The deployed application is available through:

http://a2f548479cd504fb4b5b3b1e1aad253b-1757595433.ap-south-1.elb.amazonaws.com:3000

Important Kubernetes Service Details

The Kubernetes service:

trend-app-service

was exposed as:

LoadBalancer

and forwarded traffic to application port 3000.

Deployment Troubleshooting

During the pipeline setup, the EKS deployment initially failed because the CodePipeline service role was not authorized to access the EKS cluster.

The issue was resolved by adding the CodePipeline service role as an IAM access entry in the trend-cluster.

After the access entry was created, the pipeline was retried and the Source, Build, and Deploy stages completed successfully.

Repository Contents

The repository contains deployment-related files including:

Dockerfile

buildspec.yml

deployment.yaml

service.yaml

dist/

AWS/Kubernetes related deployment assets

Submission Checklist

GitHub repository link

CI/CD pipeline created

GitHub Source stage configured

AWS CodeBuild stage configured

Amazon EKS deployment configured

Kubernetes LoadBalancer created

Application successfully opened through LoadBalancer

Load Balancer ARN obtained

Add screenshots to the submission document

Final Submission Values

GitHub Link:https://github.com/abhaybhadauriya123/Trend

Kubernetes LoadBalancer ARN:arn:aws:elasticloadbalancing:ap-south-1:080641083688:loadbalancer/a2f548479cd504fb4b5b3b1e1aad253b

Application URL:http://a2f548479cd504fb4b5b3b1e1aad253b-1757595433.ap-south-1.elb.amazonaws.com:3000
