#Update 1
# Coworking Space Service Extension
The Coworking Space Service is a set of APIs that enables users to request one-time tokens and administrators to authorize access to a coworking space. This service follows a microservice pattern and the APIs are split into distinct services that can be deployed and managed independently of one another.he API provides business analysts with basic analytics data on user activity in the coworking space service. The application they provide you functions as expected, and you will help build a pipeline to deploy it to Kubernetes. You'll submit artefacts from the build and deployment of this service.


# Step 1: Set Up a Postgres Database 
Pre-requisites:
- Have Kubernetes cluster ready.
- Have `kubectl` installed and configured to interact with your cluster.
- Have postgres installed.

Instructions:
1. Install postgres:
   ```bash
   kubectl apply -f pvc.yaml
   kubectl apply -f pv.yaml
   kubectl apply -f postgresql-deployment.yaml
   ```
2. Verify the Installation:
   ```bash
   kubectl get pods
   ```
5. Get the PostgreSQL Connection Details:
   ```bash
   export POSTGRES_PASSWORD=$(kubectl get secret --namespace default my-postgres-postgresql -o jsonpath="{.data.postgres-password}" | base64 --decode)
   ```

## Create a Dockerfile for the Python Application
Dockerfile
[Dockerfile](./Dockerfile)

## Write a Build Pipeline with AWS CodeBuild

buildspec File
[buildspec](./buildspec.yml)

BulidCode history
![BulidCode history](Project%20screenshots/codebuild.png)

## Create Kubernetes Service and Deployment
1. List Services
   ```bash
   kubectl get svc
   kubectl describe svc
   ```
   List Services
   ![List Services](Project%20screenshots/ListServices.png)
   List Describe Services Kubernetes
   ![List Describe Services Kubernetes](Project%20screenshots/DescribeSvcKubernetes.png)
   List Describe Services Postgres DB
   ![List Describe Services Postgres DB](Project%20screenshots/DescribeSvcMy-postgres-postgresql.png)
   List Describe Services Project3 API
   ![List Describe Services Project3 API](Project%20screenshots/DescribeSvcProject3-api.png)

3. List Pods
   ```bash
   kubectl get pods
   kubectl describe pods
   ```
   List Pods
   ![List Pods](Project screenshots/ListPods.png)
   List Describe Pods DB
   ![List Describe Pods DB](Project%20screenshots/GetPodsDescribeMy-postgres-postgresql-0.png)
   List Describe Pods API
   ![List Describe Pods API](Project%20screenshots/GetPodsDescribeProject3-api-dbd9446-smh74.png)
   
4. List Deployments
   ```bash
   kubectl get deployments
   kubectl describe deployment project3-api
   ```
   List Deployments
   ![List Deployments](Project%20screenshots/ListDeployments.png)
   List Describe Deployments
   ![List Describe Deployments](Project%20screenshots/ListDescribeDeployments.png)

## AWS CloudWatch for Logs
   
   CloudWatch Cluster Logs
   ![CloudWatch Cluster Logs](Project%20screenshots/CloudWatch-ClusterLogs.png)
   CloudWatch Logs
   ![CloudWatch Logs](Project%20screenshots/CloudWatch-Logs.png)
