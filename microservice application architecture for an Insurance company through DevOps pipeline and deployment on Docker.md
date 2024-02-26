# **To create a microservice application architecture for an Insurance company through DevOps pipeline and deployment on Docker.**

# Problem Statement and Motivation
## ASI Insurance is facing challenges in improving the SLA to its customers
## due to its organizational growth and existing monolithic application architecture. 
## It requires transformation of the existing architecture to a microservice application architecture,
## while also implementing DevOps pipeline and automations. 
## The successful completion of the project will enable ASI Insurance to 
## improve its overall application deployment process, enhance system
## scalability, and deliver better products and services to its customers.

## Industry Relevance

## **Skills used in the project and their usage in the industry are as below:**
## • Jenkins: It is used for continuous integration and continuous delivery.  In this project, Jenkins can be used to automate the entire software delivery process.
## • GitHub: It is a web-based hosting service that provides a Git repository management system. In this project, it is used to manage the source code of the microservices and facilitating the development process.
## • Docker Hub: It is a cloud-based repository for storing, managing, and sharing Docker container images. In this project, it is used to store the Docker image and use to deploy the same on cloud.
## • Amazon Web Service: It is a cloud platform that provide necessary computation and storage resources to host an application. In this project, we will deploy our application on an EC2 instance.

## Task (Activities)
## 1. Create the Dockerfile, Jenkinsfile, Ansible playbook, and the source file of the static website
## 2. Upload all the created files to GitHub
## 3. Go to the terminal and install NodeJS 16
## 4. Open the browser and access the Jenkins application
## 5. Create Jenkins pipeline to perform CI/CD for a Docker container
## 6. Create Docker Hub Credentials and other necessary pre-requisites 
##        before running  build
## 7. Set up Docker remote host on AWS and configure deploy stage in pipeline
## 8. Execute Jenkins Build
## 9. Access deployed application on Docker container

## Step 1: Provisioned a Jenkins Server Using Terraform
## Installed terraform
```
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list

sudo apt update

sudo apt install terraform
```
![Screenshot 2024-02-25 234155](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/1838d70c-3833-4e81-b95d-80ea4b41e86c)

![Screenshot 2024-02-25 234439](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/f3f6b1ec-e633-44ce-a2bb-39ca73b2b113)

![Screenshot 2024-02-25 234459](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/1f1e40aa-adc4-4a42-9087-f2d200f35dd8)

![Screenshot 2024-02-25 234945](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/ca2a6614-22b5-4bf5-9094-9ab7c1d186cd)

## Installed aws cli
```
sudo apt update -y
sudo apt install awscli
```
![Screenshot 2024-02-25 235631](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/ce4480c9-deaf-4887-aa26-c95c62cdadc2)

![Screenshot 2024-02-25 235658](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/9b06e0c4-2996-4999-be24-64fe297ef925)

## aws --version




## 1.1  created a user called Test-user On the AWS Console and gave an administrator access permission. TAccess keys and secret access keys were then generated
## 1.2  From the terraform documentation, established the below code to launch an Ec2 Instance-Jenkins server
```
resource "aws_instance" "web" {

  ami           = "ami-0c7217cdde317cfec"

  instance_type = "t2.medium"



  tags = {

    Name = "Jenkins-Sever"

  }

}
```
## 1.3 Run AWS configure on the terminal as a securirty measure where the Access keys and Secrect Access keys generated were saved
## 1.4 initialized the working directory with terraform init command. 
## **terraform init**

![Screenshot 2024-02-26 000313](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/b26d5b2b-000c-49ed-b252-86b085f1fd12)

## 1.5 terraform plan to create an execution plan
## **terraform plan**

![Screenshot 2024-02-26 000623](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/879525df-af6e-4825-a49b-be9435b481a2)

![Screenshot 2024-02-26 000634](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/6da49584-f48c-48a3-839c-6c2dc237d0b3)

## terraform apply command to apply changes required to reach the desired state of the configuration.
## **terraform apply**

![Screenshot 2024-02-26 000957](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/1649b4db-0e37-40a7-8909-051817641e1f)

![Screenshot 2024-02-26 001009](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/85fdead7-e28e-4fd5-a883-6f3a7de63b93)

![Screenshot 2024-02-26 001157](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/3bfa4a41-545a-46ed-8501-483c1aa3e487)





