# **Objective: To deploy a voting application in Kubernetes.**

## **Tools used**: kubeadm, kubectl, kubelet, and etcd

## **Prerequisites**: A Kubernetes cluster was set up 

## **Steps followed:**

## 1.	Created a namespace
## 2.	Created the application
## 3.	Verified the Deployment of application


## **Step 1: Created a namespace**
## 1.1	Created a namespace **vote**, using the following command:
## **kubectl create namespace vote**

![Screenshot 2024-01-27 044911](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/62af93de-1273-494a-8e17-084aaa14946c)


## **Step 2: Created the application**
## 2.1	Cloned the following repository for a voting app.
## **git clone https://github.com/dockersamples/example-voting-app.git**

![Screenshot 2024-01-27 051721](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/da22dfd5-9016-48ce-a9ec-dca7878235cf)


## 2.2	Changed Directory to the cloned Location.

## **cd example-voting-app/**

## 2.3	Created the application by running the following command:
## **kubectl create -f k8s-specifications/**

![Screenshot 2024-01-27 055716](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/eff36782-d569-450c-93b9-85928454c40f)

## 2.4 Deployed the Application
## **ls**
## **ls k8s-specifications**

![Screenshot 2024-01-27 063149](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/cfc1c33b-a67f-41d7-ad93-1ded2912cbdb)

## Deployed all the components yaml file in the directory by running the following commands:
## Database Component:
## **kubectl apply -f k8s-specifications/db-deployment.yaml -n vote**
## **kubectl apply -f k8s-specifications/db-service.yaml -n vote**
## Redis Component:
## **kubectl apply -f k8s-specifications/redis-deployment.yaml -n vote**
## **kubectl apply -f k8s-specifications/redis-service.yaml -n vote**
## Result Service Component:
## **kubectl apply -f k8s-specifications/result-deployment.yaml -n vote**
## **kubectl apply -f k8s-specifications/result-service.yaml -n vote**
## Vote Service Component:
## **kubectl apply -f k8s-specifications/vote-deployment.yaml -n vote**
## **kubectl apply -f k8s-specifications/vote-service.yaml -n vote**
## Worker Component:
## **kubectl apply -f k8s-specifications/worker-deployment.yaml -n vote**

![Screenshot 2024-01-27 070637](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/6747f4fb-9c3b-45d7-8348-3cfe6ff5e025)

## Verified the Status of the pod:
## *kubectl get pods -n vote**

![Screenshot 2024-01-27 071114](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/492a63bb-05a3-44af-8c4a-736f5008499c)


## **Step 3: Verified the Deployment of application**
## 3.1	Verify the created Pod state using the following command:

## **kubectl get pod -n vote -o wide**

![Screenshot 2024-01-27 071315](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/6679f7a7-68ac-45b4-b211-4d2147c03366)

## 3.2	Verify the Deployment.

## **kubectl get deployment -n vote**

![Screenshot 2024-01-27 071926](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/c6949c2c-c178-4f38-9a64-d85fbcb83aa7)

## The following Commands gives the detailed Information of the pods with the namespace role:
## **kubectl get pod --namespace vote -o wide**

## **kubectl get svc --namespace vote -o wide**

![Screenshot 2024-01-27 073743](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/b821fc19-4b01-4aa3-9421-1504688ce435)

## Verify on which node the pod is running.
## **kubectl get nodes -o wide**

![Screenshot 2024-01-27 074343](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/162e09a6-e48f-4f8e-860f-c1a24f60b23d)







