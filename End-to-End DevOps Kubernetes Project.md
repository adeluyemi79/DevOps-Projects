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
## created an instance(jenkins Server) selecting Ubuntu 22.04 version as the os, t2 Instance Large type as multiple things were Configured on the Jenkins Server and allowing All Inbound and Outbound traffic from anywhere on the Security Group.
