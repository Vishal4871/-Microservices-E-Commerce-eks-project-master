Project Overview

This project is a Microservices-based E-Commerce Application deployed on AWS EKS (Elastic Kubernetes Service). It demonstrates how a real-world scalable e-commerce system can be designed using Docker, Kubernetes, AWS services, and CI/CD practices.

The application is divided into multiple independent microservices such as User, Product, Order, Payment, and Cart, each deployed as a separate Kubernetes service. The architecture ensures scalability, fault tolerance, and easy maintenance.



Architecture

.Frontend: React / Web UI (Containerized)

.Backend: Multiple Microservices (REST APIs)

.Containerization: Docker

.Orchestration: Kubernetes (EKS)

.Cloud Provider: AWS

.Networking: Kubernetes Services & Ingress

.Database: MongoDB / MySQL (Containerized or Managed)

.CI/CD: GitHub + Jenkins / GitHub Actions (Optional)


Tech Stack

.AWS EKS

.Docker & Docker Hub

.Kubernetes (kubectl, manifests)

.AWS CLI & eksctl

.Helm (optional)

.Nginx Ingress Controller

.Git & GitHub.


 Project Structure

Microservices-E-Commerce-eks-project-master/
│
├── frontend/
│ └── Dockerfile
│
├── services/
│ ├── user-service/
│ ├── product-service/
│ ├── order-service/
│ ├── payment-service/
│ └── cart-service/
│
├── k8s-manifests/
│ ├── deployments/
│ ├── services/
│ └── ingress.yaml
│
├── scripts/
│ └── eks-setup.sh
│
└── README.md



Prerequisites

.Before starting, make sure you have:

.AWS Account

.AWS CLI configured

.eksctl installed

.kubectl installed

.Docker installed

.Git installed.



Create EKS Cluster

  eksctl create cluster \
--name ecommerce-cluster \
--region ap-south-1 \
--nodegroup-name standard-workers \
--node-type t3.medium \
--nodes 2


Verify cluster:
.kubectl get nodes

Build & Push Docker Images

docker build -t vishalkumar/user-service ./services/user-service
docker push vishalkumar/user-service


Update Kubernetes Manifests

Update image names in deployment YAML files:
image: vishalkumar/user-service:latest


Deploy Microservices to EKS

kubectl apply -f k8s-manifests/deployments/
kubectl apply -f k8s-manifests/services/

Check pods:
kubectl get pods

Apply ingress:
kubectl apply -f k8s-manifests/ingress.yaml

Access the Application
kubectl get ingress
.Copy the LoadBalancer DNS and open it in the browser.


Features

.Microservices Architecture

.Independent scaling of services

.Containerized deployment

.Kubernetes orchestration

.AWS EKS production-ready setup

.CI/CD ready.


Common Issues & Fixes

.Pods not starting → Check logs using kubectl logs

.ImagePullBackOff → Verify Docker image name

.Ingress not working → Check LoadBalancer status