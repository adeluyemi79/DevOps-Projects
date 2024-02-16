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

## 4.3 Set the permissions
## To grant permission to access the host server machine, open the exports file in the /etc directory:
## sudo nano /etc/exports
## Inside the file, append the following code:
## /mydbdata 	*(rw,sync,no_root_squash)

![Screenshot 2024-02-15 151852](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/677be625-e5e3-44cd-88c8-0a3033328cf3)

![Screenshot 2024-02-15 152749](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/e23eea19-c35e-4a48-86f8-64458ffdacf8)

## 4.4 export all shared directories defined in the /etc/exports file, use:
## **sudo exportfs -rv**

## 4.5	Made the folder publicly accessible by changing its owner user and group:
## sudo chown nobody:nogroup /mydbdata/

## 4.6	Assigned full permissions to ensure everyone can read, write, and execute files in this directory:
## sudo chmod 777 /mydbdata/

## 4.7	Restarted the NFS kernel server to apply the changes:

## sudo systemctl restart nfs-kernel-server

![Screenshot 2024-02-15 153836](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/cf0d35a9-6378-475d-9c2e-2d1fa055b4e4)

## 4.8	Retrieved the internal IP of the node where NFS Server is installed, which will be used to link the PV

## **ip a**

![Screenshot 2024-02-15 154249](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/c9155946-f431-41cb-8e8c-cfa0ef4ba5fb)


## The Ip 172.31.27.25 used to associate the PV with the NFS server

## Task 5: Configured the NFS common on client machines
## This action was performed on each worker node

## Run the following command to install the NFS common package:
## **sudo apt install nfs-common**

![Screenshot 2024-02-15 155239](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/60553662-89c8-42f3-80a5-5b3f62a14086)

## Refreshed the NFS common service and verify its current status:

## sudo rm /lib/systemd/system/nfs-common.service
## sudo systemctl daemon-reload

## sudo systemctl restart nfs-common
## sudo systemctl status nfs-common

![Screenshot 2024-02-15 155804](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/cca1838f-e43e-41ac-82c7-0dc3e4c9617a)

![Screenshot 2024-02-15 160306](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/7a7e553b-2f78-46bc-984a-727f2607fd09)

## Task 6: Created the PersistentVolume

 ## On the master node, drafted the following YAML for the PV and save it as pv.yaml:

## vi pv.yaml
```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: test
  labels:
    app: wordpress
spec:
  capacity:
    storage: 10Gi
  accessModes:
    - ReadWriteMany
  nfs:
    server: 172.31.27.25
    path: "/mydbdata"
```

## **kubectl apply -f pv.yaml**

## **kubectl get pv**

![Screenshot 2024-02-15 161609](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/96c9599d-6941-45d9-8f3b-1bc2ea3df50e)

## 6.1: Created the PersistentVolumeClaim

## vi pvc.yaml
```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mypvc1
  labels:
    app: wordpress
spec:
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: 6Gi
```

![Screenshot 2024-02-15 162346](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/3efea018-e603-4f08-87bc-9f5bb9f1c387)



## Task 7: Created a secret for MySQL deployments secret data

## Created a YAML manifest file for the secret:

## mysql-secret.yaml:

```
apiVersion: v1
kind: Secret
metadata:
  name: mysql-secret
type: Opaque
data:
  MYSQL_ROOT_PASSWORD: base64-encoded-password
```
## Replaced base64-encoded-password with the Base64 encoded version of the MySQL root password. generated the Base64 encoded value of the password using the following command:

## **echo -n 'your-password' | base64**

## Applied the YAML manifest to create the secret

## kubectl apply -f mysql-secret.yaml

![Screenshot 2024-02-15 170607](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/847ad803-69c0-4514-a133-810b8d1fc154)


## Task 8: Created a configmap for WordPress deployment to store non-sensitive information

## Created a YAML Manifest File:
## Create a YAML file named wordpress-configmap.yaml and add the following content:
## Generated a password for the wordpress

 ## openssl rand -base64 12

## vi wordpress-configmap.yaml

```
apiVersion: v1
kind: ConfigMap
metadata:
  name: wordpress-configmap
data:
  WORDPRESS_DB_HOST: mysql-service
  WORDPRESS_DB_NAME: wordpress-db
  WORDPRESS_DB_USER: wordpress-user
  WORDPRESS_DB_PASSWORD: your-password
```

## Replaced your-password with the Generated Password

## Applied the Yaml Manifest to create the ConfigMap
## kubectl apply -f wordpress-configmap.yaml

![Screenshot 2024-02-15 172836](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/32b7b3a8-265d-49e4-8d76-d436420ca7e2)

 ## Created Deployment for WordPress

## wordpress.yaml 

```
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: wordpress
  name: wordpress
spec:
  replicas: 1
  selector:
    matchLabels:
      app: wordpress
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: wordpress
    spec:
      containers:
      - image: wordpress
        name: wordpress
        env:
        - name: WORDPRESS_DB_HOST
          value: mysql
        - name: WORDPRESS_DB_PASSWORD
          value: simplilearn
        - name: WORDPRESS_DB_USER
          value: root
        - name: WORDPRESS_DB_NAME
          value: database1
        resources: {}
status: {}
```
## kubectl create -f wordpress.yaml

## Created a Deployment for mysql
## vi mysql.yaml

```
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: mysql
  name: mysql
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mysql
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: mysql
    spec:
      containers:
      - image: mysql:5.6
        name: mysql
        env:
        - name: MYSQL_ROOT_PASSWORD
          value: simplilearn
        - name: MYSQL_DATABASE
          value: database1
        resources: {}
status: {}
```
## Kubectl get pods
## kubectl get deployments

## Exposed Service for WordPress and MySQL Deployment
## To expose Service for WordPress and MySQL Deployment, run the following commands:
## kubectl expose deployment mysql --port=3306
## kubectl expose deployment wordpress --port=80

![Screenshot 2024-02-15 181150](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/dca2d6c3-87de-4d30-9232-da3ab1da5fec)

## Change the Service type for both MySQL and WordPress from ClusterIP to Nodeport.

## kubectl edit svc mysql

![Screenshot 2024-02-15 181658](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/f4c3ed14-3502-4824-9783-d85eb610d099)

## kubectl edit svc wordpress  

![Screenshot 2024-02-15 181922](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/4b70a025-dd1a-47a3-9f10-e72bf4cf6aca)

![Screenshot 2024-02-15 182055](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/53ccd6bb-8ef8-4138-ae57-976c700bcc09)

## kubectl get svc
## kubectl get pods -o wide
## kubectl get nodes -o wide

![Screenshot 2024-02-15 183200](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/1c49ec57-e4d6-4191-a1a7-a34b004db39c)

## Verified the Deployment of application
## Pasted worker-node-1 ip and the Nodeportof the wordpress: 172.31.27.25:30678 onto a browser using the kubernetes desktop mode

## Installed my Mysql-server
## sudo apt-get install mysql-server
## Start my mysl-server
## sudo systemctl start mysql

![Screenshot 2024-02-15 185942](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/4d5a19c1-0f97-4ec6-9404-5b5f6e60f008)

![Screenshot 2024-02-15 191002](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/39af5d06-253d-4bf9-b7f6-34e35f1c7781)

![Screenshot 2024-02-15 195027](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/93b731d4-c853-451b-a813-7373e232b8fe)


![image](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/f4f2cd06-751e-4199-b974-5d7c2ee2e4f9)






























