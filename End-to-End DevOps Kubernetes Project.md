# **End-to-End DevOps Kubernetes Project**

![image](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/792dce9b-748a-4507-82d7-3447b48bbe8e)

# **Prerequisites:**
## Basic understanding of Kubernetes concepts.
## Access to AWS or any other cloud provider for server instances.
## A TMDB API key for accessing movie databases in your Netflix Clone application.
## DockerHub account for pushing and pulling Docker images.
## Gmail account for email notifications.
## Jenkins, Kubernetes, Docker, and necessary plugins installed.

# **High-Level Overview:**
## Infrastructure Setup: Provisioned servers for Jenkins, Monitoring, and Kubernetes nodes.
## Toolchain Integration: Integrated essential tools like Jenkins, SonarQube, Trivy, Prometheus, Grafana, and OWASP Dependency-Check.
## Continuous Integration/Continuous Deployment (CI/CD): Automated workflows with Jenkins pipelines for code analysis, building Docker images, and deploying applications on Kubernetes.
## Security Scanning: Implemented Trivy and OWASP Dependency-Check to scan for vulnerabilities in code and Docker images.
## Monitoring and Visualization: Set up Prometheus and Grafana for real-time monitoring and visualization of both hardware and application metrics.
## Email Notifications: Configured Jenkins for email alerts based on pipeline results.

## OWASP Dependency-Check(**Open Web Application Security Project Dependency-Check**) is an open-source tool that scans project dependencies to identify known, publicly disclosed, and critical vulnerabilities. It helps developers and security professionals identify and mitigate security issues in third-party libraries and components used in a software project.

## **Key features of OWASP Dependency-Check include:**

## Dependency Analysis: The tool analyzes project dependencies, including libraries and components, to identify potential security vulnerabilities.

## Vulnerability Detection: It checks dependencies against a comprehensive database of known vulnerabilities, including the National Vulnerability Database (NVD) and various other sources.

## Integration with Build Tools: Dependency-Check integrates with popular build tools such as Apache Maven, Gradle, and Jenkins, making it easy to incorporate into the development and build process.

## Multiple Language Support: It supports various programming languages, making it versatile for projects developed in different technologies.

## Automation: Dependency-Check can be automated within the build process to provide continuous monitoring of dependencies for security issues.

## Customizable Reporting: The tool generates reports highlighting identified vulnerabilities, severity levels, and other relevant information. Reports can be customized based on project requirements.

## Integration with Security Scanners: It can be used in conjunction with other security tools and scanners to provide a more comprehensive security analysis.

## Command Line and GUI: Dependency-Check can be used through the command line for automation or through a graphical user interface (GUI) for manual analysis.

# **Launched for servers for this Project**

## Jenkins Server- On this Server, Jenkins will be installed with some other tools such as sonarqube(docker container), trivy, and kubectl.

## Monitoring Server- This Server will be used for Monitoring where we will use Prometheus, Node Exporter, and Grafana.

## Kubernetes Master Server- This Server will be used as the Kubernetes Master Cluster Node which will deploy the applications on worker nodes.

## Kubernetes Worker Server- This Server will be used as the Kubernetes Worker Node on which the application will be deployed by the master node.

## **Jenkins Server**
## created an instance(jenkins Server) selecting Ubuntu 22.04 version as the os, t2 Instance Medium type as multiple things were Configured on the Jenkins Server and allowing All Inbound and Outbound traffic from anywhere on the Security Group. storage volume of 35GB

![Screenshot 2024-02-01 121110](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/26c7b130-58ab-4275-adcd-2733d361a579)

## **Monitoring Server**
## Provisioned an instance(monitoring Server) selecting Ubuntu 22.04 version as the os, t2 Medium Instance type and allowing all inbound and outbound traffic from anywhere on the security Group.

## **Kubernetes Master & Worker Node**

## Provisioned two Instances,one for the Master and the other for the worker Node.
## Selected The Ubuntu 22.04 version as os and a t2 medium Instance type.

## Connected to the Jenkins-Server Via SSH

![Screenshot 2024-02-01 123932](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/1669fc01-9adc-412f-97d3-32ef57502198)
## set Hostname for the Jenkins-Server
## **sudo hostnamectl st-hostname Jenkins 
## /bin/bash

![Screenshot 2024-02-01 124903](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/bc98ae03-6ea3-4bd3-b0b4-4336f91cad6c)

## Download Open JDK and Jenkins
## Installed Java

## **sudo apt update -y**
## **sudo apt install openjdk-11-jre -y**
## **java --version**

![Screenshot 2024-02-01 125657](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/157e5b51-a581-48ac-9351-93f3784a6369)

![Screenshot 2024-02-01 125901](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/4bc8fa58-53f2-4309-b084-921b63ae4237)

![Screenshot 2024-02-01 125933](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/c3875f6b-3c56-48a3-936c-53a84fa9e4ad)

## Installed Jenkins
## **curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \**
##  **/usr/share/keyrings/jenkins-keyring.asc > /dev/null**
## **echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \**
 ## **https://pkg.jenkins.io/debian binary/ | sudo tee \**
  ## **/etc/apt/sources.list.d/jenkins.list > /dev/null**
## **sudo apt-get update -y**
## **sudo apt-get install jenkins -y**

![Screenshot 2024-02-01 130510](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/e023bbb4-4192-421e-a63a-603516b3ebb3)

![Screenshot 2024-02-01 130958](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/cf13945b-fddf-4e6b-b217-21c83e2c43cb)
## **service Jenkins status**

![Screenshot 2024-02-01 131255](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/34efbb65-8d63-4273-b4f6-41242e21fda5)

## Copied the Jenkins Server Public IP and pasted it on a browser with port number 8080.

![Screenshot 2024-02-01 131618](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/b968f990-7583-4627-8320-d664f872286d)

## Ran this command on Jenkins server

## **sudo cat /var/lib/jenkins/secrets/initialAdminPassword**
## Copied the output and pasted it into the above snippet text field and click on Continue.

![Screenshot 2024-02-01 132201](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/112570e3-af54-4eb9-8b9e-8994da9560f2)

![Screenshot 2024-02-01 132359](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/e51d9ef7-7405-44ad-b4e0-f1d95c616c9d)









