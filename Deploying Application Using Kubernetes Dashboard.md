# **Deploy the Application Using the Kubernetes Dashboard**


## **Course-end Project 1**
## Description
## Objectives
## To deploy a multi-tier PHP and MySQL application using Kubernetes with specific configurations for user roles, storage, service verification, namespace restrictions, quota limits, and data management.
## Problem Statement and Motivation
## **Real-Time Scenario:**

## Karen is a DevOps engineer at a tech startup. Her team has developed a new application using PHP and MySQL. Now, it is her task to deploy that application.
## The company plans to utilize Kubernetes for its robust container orchestration capabilities.
## Karen must create a Kubernetes dashboard with specific configurations, user roles, storage, service verification, and data management.
## Industry Relevance :

## The following tools utilized in this project are widely applied in the industry:
## 1. kubeadm: A utility that offers kubeadm init and kubeadm join as efficient ways to bootstrap Kubernetes clusters. It focuses on bootstrapping rather than machine provisioning.
## 2. kubectl: A command-line interface for Kubernetes that allows execution of commands against Kubernetes clusters. It can be used for deploying applications, managing cluster resources, and viewing logs.
## 3. kubelet: An essential node agent present on every node in a Kubernetes cluster. It ensures that the containers described in the provided PodSpecs are running and healthy.
## 4. Docker: Docker is a tool designed to facilitate developers in building, sharing, and running applications in containers. It takes care of the setup, allowing developers to concentrate on the code.

# **Tasks**

## **The following tasks outline the application using Kubernetes:**

## 1. Getting started with pods, services, and deployments
## 2. Creating and verifying the service
## 3. Creating a token and working on a dashboard
## 4. Configure the NFS-server for MySQL and WordPress deployment
## 5. Setting up the NFS client side
## 6. Creating and verifying the PV
## 7. Creating a secret for MySQL deployments secret data
## 8. Creating a configmap for WordPress deployment to store non-sensitive information

## Task 1: created a YAML manifests for the application's pods, services, and deployments. 

## Pod Manifest (php-app-pod.yaml):
```
apiVersion: v1
kind: Pod
metadata:
  name: php-app
spec:
  containers:
  - name: php-app-container
    image: your-php-image
    ports:
    - containerPort: 80
```

## Service Manifest (php-app-service.yaml):
```
apiVersion: v1
kind: Service
metadata:
  name: php-app-service
spec:
  selector:
    app: php-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
```

## Deployment Manifest (mysql-deployment.yaml):

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mysql
  template:
    metadata:
      labels:
        app: mysql
    spec:
      containers:
      - name: mysql-container
        image: mysql:latest
        env:
        - name: MYSQL_ROOT_PASSWORD
          value: your-root-password
        ports:
        - containerPort: 3306
```

## Deployment Command:

```
kubectl apply -f php-app-pod.yaml
kubectl apply -f php-app-service.yaml
kubectl apply -f mysql-deployment.yaml
```

![Screenshot 2024-02-15 102317](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/483eca8b-d4a3-46bd-a548-6390d8eac13d)

## Task 2:  Verified the services

## kubectl get svc php-app-service

![Screenshot 2024-02-15 103544](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/b60aba60-cb00-4109-9f73-2bc85d65cb1a)

## Task 3: created a service account and generated a token for accessing the Kubernetes dasshboard:

## Step1: Implement the dashboard deployment

## **kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml**

![Screenshot 2024-02-15 110005](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/f1d5e2bd-b0f4-41a9-85a4-d2dca0545695)


## Step 2: Validate the pod, service, and deployment creation
## Used the Following commands to verify if the pods, services, and deployments have been created:

## kubectl get pods -n kubernetes-dashboard -o wide
## kubectl get deployment -n kubernetes-dashboard -o wide
## kubectl get svc -n kubernetes-dashboard -o wide

![Screenshot 2024-02-15 110330](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/016da3d6-f826-4a00-841b-28dd2027d823)

## 2.1  To access the service outside the cluster, edit the service type from ClusterIP to NodePort using the following command:

## kubectl edit svc -n kubernetes-dashboard kubernetes-dashboard

```
# Please edit the object below. Lines beginning with a '#' will be ignored,
# and an empty file will abort the edit. If an error occurs while saving this file will be
# reopened with the relevant failures.
#
apiVersion: v1
kind: Service
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"v1","kind":"Service","metadata":{"annotations":{},"labels":{"k8s-app":"kubernetes-dashboard"},"name":"kubernetes-dashboard","namespace":"kubernetes-dashboard"},"spec":{"ports":[{"port":443,"targetPort":8443}],"selector":{"k8s-app":"kubernetes-dashboard"}}}
  creationTimestamp: "2024-02-15T15:59:45Z"
  labels:
    k8s-app: kubernetes-dashboard
  name: kubernetes-dashboard
  namespace: kubernetes-dashboard
  resourceVersion: "288156"
  uid: fbdf86cc-43b6-471f-a293-80db57379c7c
spec:
  clusterIP: 10.99.33.112
  clusterIPs:
  - 10.99.33.112
  internalTrafficPolicy: Cluster
  ipFamilies:
  - IPv4
  ipFamilyPolicy: SingleStack
  ports:
  - port: 443
    protocol: TCP
    targetPort: 8443
  selector:
    k8s-app: kubernetes-dashboard
  sessionAffinity: None
  type: NodePort
status:
  loadBalancer: {}
```

![Screenshot 2024-02-15 110934](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/d8d102f8-4978-4ab8-a5c0-18c921f354a4)

![Screenshot 2024-02-15 111115](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/4081da37-1007-479a-a715-6921ef4086b8)

## 2.2 To confirm that the service type has been changed to NodePort, use the command:
## kubectl get svc -n kubernetes-dashboard -o wide

![Screenshot 2024-02-15 111512](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/66751847-8d75-43a4-b177-30291065d058)

## 2.3 To determine the location of the pod, run the following commands:
## kubectl get pods -n kubernetes-dashboard -o wide
## kubectl get svc -n kubernetes-dashboard -o wide
## kubectl get nodes -o wide

![Screenshot 2024-02-15 112204](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/00c72d9e-ffdc-4bcb-929e-87e2c5e82e8a)

## The Pod is Running on Worker-node-1

## 2.4 Use the INTERNAL-IP as 172.31.27.25, and PORT(S) as 31971, and copy the link:
## **https://172.31.27.25:31971**

## Step 3: Access the master node IP

![Screenshot 2024-02-15 134512](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/b5363a4c-12c6-4ac3-8e50-b2b9d9172731)

## Step 4: Log into the service dashboard
## 4.1 Created a service account by running the following command, and then input the code in the master node:
## **vi ServiceAccount.yaml**

```
apiVersion: v1
kind: ServiceAccount
metadata:
name: admin-user
namespace: kubernetes-dashboard
```
## 4.2 Applied the YAML file with the command:
## kubectl apply -f ServiceAccount.yaml

![Screenshot 2024-02-15 140637](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/efcdf754-6bef-4bf5-b500-f59339d90e07)

## 4.3 Create a yaml file for cluster role binding using below command and code:
## **vi ClusterRoleBinding.yaml**

```
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
name: admin-user
roleRef:
apiGroup: rbac.authorization.k8s.io
kind: ClusterRole
name: cluster-admin
subjects:
- kind: ServiceAccount
name: admin-user
namespace: kubernetes-dashboard
```

## 4.4 Run the below command to create cluster role binding:
## **kubectl apply -f ClusterRoleBinding.yaml**

## 4.5 Retrieve the token to log in by running the following command:
## kubectl -n kubernetes-dashboard create token admin-user

![Screenshot 2024-02-15 142332](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/3edff7d9-ab30-4586-b461-53486973022f)

## 4.6 Copied the token and paste it into the Kubernetes dashboard login screen, then click Sign in

![Screenshot 2024-02-15 143215](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/cfbd6bde-1d31-4163-8283-407b7b1f9fb5)

![Screenshot 2024-02-15 143637](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/8fecd142-9435-4fa1-8799-03c141ffaeec)

## Task 4: Configured the NFS-server for MySQL and WordPress deployment
## 4.1 Configure the NFS kernel server
## Created a directory on the worker-node-1 using the following command:
## **sudo mkdir /mydbdata**
## 4.2 Install the NFS kernel server on the machine:
## sudo apt install nfs-kernel-server

![Screenshot 2024-02-15 151104](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/7886e00b-7db2-4305-8913-9d79239a0db1)











