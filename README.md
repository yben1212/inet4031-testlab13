# Docker Lab: Containerizing a Three-Tier Application
**INET 4031 - Introductions to Systems**

This lab introduces Docker and Docker Compose by having you containerize a
real, multi-service application. You will package three components: Apache,
Flask, and MariaDB. These will be packaged into separate containers and wired together so they function as a complete application.

The application code and scaffolding are provided. Your job is to complete the Dockerfiles, verify the stack runs correctly, and document your work below.

> **Directions and explanations for this lab are on the repository Wiki.**
> Refer to the Wiki pages for step-by-step instructions.

---

*The sections below are for you to fill out. Replace each placeholder with your own content before submitting. Having a detailed README is the best practice for showing your work in future GitHub repositories.*

---

# Project Overview

This application is a three tier ticket tracking system. There is a web interface that is created by Apache that users can interact with to create and view support tickets. Apache forwards the requests to Flask, which reads and writes ticket data to a MariaDB database. All of the components run in seperate Docker containers.

# Prerequisites

- Docker
- Docker Compose
- A .env file with your own credentials

# Getting Started

1. Clone the repository
2. Copy the example environment file and fill in your credentials:
   cp .env.example .env
   nano .env
3. run 'docker compose up --build' to build and start the stack
4. Open a browser and navigate to http://localhost

# Configuration

Docker Compose reads credentials from a .env file that is not committed to the repository because it contains passwords. You will need to create your own .env file using .env.example as a template and fill in the following:
- DB_ROOT_PASSWORD - password for MariaDB
- DB_NAME - name of the database
- DB_USER - database user for Flask to connect with
- DB_PASSWORD - password for the database user

# Verification

To verify if the stack is running properly, check that all three containers are healthy using:
- docker compose ps
  
This should show a status of db, app, and web. db and app will show a status of 'Up' and 'healthy', while web will only show 'Up' since it does not have a healthcheck.

## Lab 13: Kubernetes and Desired State

The application from Lab 12 has been migrated from Docker Compose to Kubernetes using k3s, a lightweight Kubernetes distribution. Instead of managing containers directly, the application is now declared as Kubernetes Deployments and Services, giving it self-healing capabilities and desired state management.

## Deploying to Kubernetes

1. Create the namespace and secret:
kubectl create namespace ticket-app
bash create-secret.sh
3. Apply the Kubernetes manifests:
kubectl apply -f k8s/
4. Verify all pods are running:
kubectl get pods -n ticket-app

## Accessing the Dashboard
Open a browser and navigate to:
http://<192.168.56.10>:30080
