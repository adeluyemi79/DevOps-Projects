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
```
 sudo hostnamectl set-hostname Jenkins 
 /bin/bash
```
![Screenshot 2024-02-01 124903](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/bc98ae03-6ea3-4bd3-b0b4-4336f91cad6c)

## Download Open JDK and Jenkins
## Installed Java

```
sudo apt update -y
sudo apt install openjdk-11-jre -y
java --version
```
![Screenshot 2024-02-01 125657](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/157e5b51-a581-48ac-9351-93f3784a6369)

![Screenshot 2024-02-01 125901](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/4bc8fa58-53f2-4309-b084-921b63ae4237)

![Screenshot 2024-02-01 125933](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/c3875f6b-3c56-48a3-936c-53a84fa9e4ad)

## Installed Jenkins
```
 curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
 /usr/share/keyrings/jenkins-keyring.asc > /dev/null
 echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
 https://pkg.jenkins.io/debian binary/ | sudo tee \
 /etc/apt/sources.list.d/jenkins.list > /dev/null
 sudo apt-get update -y
sudo apt-get install jenkins -y
```

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

 Installed Docker on the Jenkins-Server
 ```
 sudo apt update
 sudo apt install docker.io -y
 sudo usermod -aG docker jenkins
 sudo usermod -aG docker ubuntu
 sudo systemctl restart docker
 sudo chmod 777 /var/run/docker.sock
```

![Screenshot 2024-02-01 133509](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/a42f62d6-d778-409a-ab32-e594ac6fa390)

## Installed Sonarqube on your Jenkins Server

## docker container used for Sonarqube

## **docker run -d --name sonar -p 9000:9000 sonarqube:lts-community**

![Screenshot 2024-02-01 133829](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/f098c0dc-d7e4-4c78-9bdc-d3c552b6fd08)

## copied the Public IP of Jenkins Server and add 9000 Port on a browser.

## The username and password is admin

![Screenshot 2024-02-01 134112](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/45f09bfd-aad2-4844-b12c-168baf6cc742)

![Screenshot 2024-02-01 134347](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/8ff17897-152e-489b-a347-4bd844e59161)

## Installed the Trivy tool on the Jenkins Server
```
sudo apt-get install wget apt-transport-https gnupg lsb-release
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | sudo apt-key add -
echo deb https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main | sudo tee -a /etc/apt/sources.list.d/trivy.list
sudo apt-get update
sudo apt-get install trivy
```

![Screenshot 2024-02-01 134817](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/487d4839-e4e8-4143-aed0-f83dbe88a971)

## Installed and Configure the Prometheus, Node Exporter, and Grafana on the Monitoring Server
## Logged on to the Monitoring Server Via SSH
## Create Prometheus user
```
sudo groupadd --system prometheus
sudo useradd -s /sbin/nologin --system -g prometheus prometheus
Create Directories for Prometheus
sudo mkdir /etc/prometheus
sudo mkdir /var/lib/prometheus
```

![Screenshot 2024-02-01 150918](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/f97dc8ad-749e-4c83-a4fd-8ea28d74a5d7)


## Downloaded prometheus and extract files

```
wget https://github.com/prometheus/prometheus/releases/download/v2.43.0/prometheus-2.43.0.linux-amd64.tar.gz
tar vxf prometheus*.tar.gz
```

![Screenshot 2024-02-01 151804](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/4c1a2c6b-a0a4-4ede-b2de-7645d8465afd)

## Navigated to the Prometheus Directory
## cd prometheus*/

## Moved the Binary Files & Set Owner

```
sudo mv prometheus /usr/local/bin
sudo mv promtool /usr/local/bin
sudo chown prometheus:prometheus /usr/local/bin/prometheus
sudo chown prometheus:prometheus /usr/local/bin/promtool
```

![Screenshot 2024-02-01 152346](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/3df4067c-35c3-4fb5-826c-d10a1969cf95)


## Moved the Configuration Files & Set Owner

```
sudo mv consoles /etc/prometheus
sudo mv console_libraries /etc/prometheus
sudo mv prometheus.yml /etc/prometheus
sudo chown prometheus:prometheus /etc/prometheus
sudo chown -R prometheus:prometheus /etc/prometheus/consoles
sudo chown -R prometheus:prometheus /etc/prometheus/console_libraries
sudo chown -R prometheus:prometheus /var/lib/prometheus
```

![Screenshot 2024-02-01 152829](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/17e4c09c-fd35-44e1-b4aa-31dde77b775b)

## The prometheus.yml file is the main Prometheus configuration file. It includes settings for targets to be monitored, data scraping frequency, data processing, and storage.

## sudo nano /etc/prometheus/prometheus.yml

## Created Prometheus Systemd Service
## sudo vi /etc/systemd/system/prometheus.service

## Included these settings to the file, save, and exit:

```
[Unit]
Description=Prometheus
Wants=network-online.target
After=network-online.target

[Service]
User=prometheus
Group=prometheus
Type=simple
ExecStart=/usr/local/bin/prometheus \
    --config.file /etc/prometheus/prometheus.yml \
    --storage.tsdb.path /var/lib/prometheus/ \
    --web.console.templates=/etc/prometheus/consoles \
    --web.console.libraries=/etc/prometheus/console_libraries

[Install]
WantedBy=multi-user.target
```


## Reload Systemd
```
sudo systemctl daemon-reload
Start Prometheus Service
sudo systemctl enable prometheus
sudo systemctl start prometheus
systemctl status prometheus.service
```
![Screenshot 2024-02-01 154509](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/e8a5bfda-ab35-4dae-aae7-dc2d282fa543)

## Access Prometheus Web Interface
## Prometheus runs on port 9090 by default so we need to allow port 9090 on the firewall, Do that using the command:
## **sudo ufw allow 9090/tcp**

![Screenshot 2024-02-01 154740](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/d6c1c182-bb19-4e3d-82b8-d37f32067ec4)

## With Prometheus running successfully,Copied the ip address of the Monitoring server with port 9090 and pasted it on a browser
# http://44.201.178.192:9090/

![Screenshot 2024-02-01 155635](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/d54893d9-809e-4f2c-92c8-fcae2b053c71)

## installed a node exporter to visualize the machine or hardware level data such as CPU, RAM, etc on our Grafana dashboard.

## wget https://github.com/prometheus/node_exporter/releases/download/v1.5.0/node_exporter-1.5.0.linux-amd64.tar.gz

## Extract the downloaded Archive

## tar -xf node_exporter-1.5.0.linux-amd64.tar.gz

## Move the node_exporter binary to /usr/local/bin:

## sudo mv node_exporter-1.5.0.linux-amd64/node_exporter /usr/local/bin
## Remove the residual files with:

## rm -r node_exporter-1.5.0.linux-amd64*

## created users and service files for node_exporter.

## For security reasons, it is always recommended to run any services/daemons in separate accounts of their own. Thus, a user account was created for the node_exporter. the -r flag is to indicate it is a system account, and set the default shell to /bin/false using -s to prevent logins.
## **sudo useradd -rs /bin/false node_exporter**

![Screenshot 2024-02-01 161456](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/cdc34902-8530-4968-9449-affafea514f7)

## created a systemd unit file so that node_exporter can be started at boot. 
## sudo vi /etc/systemd/system/node_exporter.service
## pasted the following in the text editor and saved it
```
[Unit]
Description=Node Exporter
After=network.target

[Service]
User=node_exporter
Group=node_exporter
Type=simple
ExecStart=/usr/local/bin/node_exporter

[Install]
WantedBy=multi-user.target
```
## Since  a new unit file have been created, the systemd daemonw was reloaded, and the service set to always run at boot and start it :
```
sudo systemctl daemon-reload
sudo systemctl enable node_exporter
sudo systemctl start node_exporter
sudo systemctl status node_exporter
```

![Screenshot 2024-02-01 162626](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/0395b9b5-8311-4ecb-bbba-14fe82c8e2b3)

## added a node exporter to the Prometheus target section. So, we will be able to monitor our server.

## edit the file

## sudo vim /etc/prometheus/prometheus.yml
## Copy the content in the file

```
# my global config
 global:
 scrape_interval: 15s # Set the scrape interval to every 15 seconds. Default is every 1 minute.
 evaluation_interval: 15s # Evaluate rules every 15 seconds. The default is every 1 minute.
 # scrape_timeout is set to the global default (10s).

 # Alertmanager configuration
 alerting:
 alertmanagers:
   - static_configs:
       - targets:
         # - alertmanager:9093

 # Load rules once and periodically evaluate them according to the global 'evaluation_interval'.
 rule_files:
 # - "first_rules.yml"
 # - "second_rules.yml"

 # A scrape configuration containing exactly one endpoint to scrape:
 # Here it's Prometheus itself.
 scrape_configs:
 # The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
  - job_name: "prometheus"

 # metrics_path defaults to '/metrics'
 # scheme defaults to 'http'.

static_configs:
 - targets: ["localhost:9090"]

 - job_name: "node_exporter"
   static_configs:
    - targets: ["localhost:9100"]
```


## After saving the file, validated the changes that was made using promtool.

```
promtool check config /etc/prometheus/prometheus.yml
Restart the Prometheus server with this command
sudo systemctl restart prometheus.service
```

![Screenshot 2024-02-01 165450](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/b36886f7-7680-48fc-8740-a7bc65df74d8)

# Checked node target on Prom GUI at http://44.201.178.192:9090/targets

![Screenshot 2024-02-01 165754](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/1eacb01c-cba2-4d09-8c15-76392a14d840)

## installed the Grafana tool to visualize all the data that is coming with the help of Prometheus.

## sudo apt-get update

## Add the Grafana repository to your Ubuntu installation:

```
sudo apt-get install -y apt-transport-https
sudo apt-get install -y software-properties-common wget
sudo wget -q -O /usr/share/keyrings/grafana.key https://apt.grafana.com/gpg.key
echo "deb [signed-by=/usr/share/keyrings/grafana.key] https://apt.grafana.com stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
```

![Screenshot 2024-02-06 145601](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/ebe79a89-8ce5-48ba-a588-5af1544551bb)

![Screenshot 2024-02-06 150325](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/d7d79d5a-e476-45d7-bdf7-6ca31221ca8e)


## Install Grafana as a service
```
sudo apt-get Update
sudo apt-get install grafana
```

![Screenshot 2024-02-06 150941](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/003531f5-0920-4fd3-ab3a-d122f2b17294)

![Screenshot 2024-02-06 151055](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/865c7b4f-1ffb-46ea-bd7f-8efd77e7205b)

## **grafana-server -v**

## Start the Grafana service using the following command:

## **sudo systemctl start grafana-server**
## Enabled the Grafana service to start on boot:

## To start it and make sure that the service is always available every time the machine is restarted, type the command:

## **sudo systemctl enable grafana-server**

## Verified the Grafana installation

## **sudo systemctl status grafana-server**

![Screenshot 2024-02-06 151833](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/04fa44a3-0bd5-412b-a57d-817c16f62229)

## Allowed Grafana TCP port 3000 in the Firewall

## Grafana's default HTTP port is 3000, allowed access to this port on the firewall.

## **sudo ufw allow 3000/tcp**

## Grafana was successfully Insatlled. Used it to create dashboards and visualize data.

## Set up Grafana
## Access the Grafana web UI by visiting http://localhost:3000 in the web browser using the Ip of the Monitoring server

## http://3.83.224.209:3000/

![Screenshot 2024-02-06 152545](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/85e2f608-a4e6-4506-bcf2-dbd9eb9ddf24)

## Logged in to Grafana with the default credentials (username: admin, password: admin)

![Screenshot 2024-02-06 152828](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/d7b82062-83a7-4d76-a674-62b90d8c8f22)

## Click on Data sources and selected the prometheus
## The Public IP of the Monitoring Server with port 9090 was provided to monitor the Monitoring Server.
## Save and test

![Screenshot 2024-02-06 153938](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/283bea96-d646-4c83-8b0c-e7b447d36761)

![Screenshot 2024-02-06 154052](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/ca259db7-1ff9-4e78-8f30-cb77d4ad78fe)

## selected import Dashboard on the Grafana Dashboard, Added 1860 for the node exported dahboad then load.

![Screenshot 2024-02-06 154627](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/dfa31687-aa8d-4e90-a9b6-ed1751f23cce)

![Screenshot 2024-02-06 154727](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/068eb918-1030-4c26-b859-7c17d353911e)

![Screenshot 2024-02-06 154840](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/4b97b87b-841d-4aab-a44f-1385ee22e153)

## selected prometheus from the drop down menu and import

![Screenshot 2024-02-06 155139](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/496944d8-0c65-4cd5-83d5-d5e6760b7b82)

![Screenshot 2024-02-06 155320](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/59d4e64b-f094-458b-b348-919f9bf95f4d)

## Installed the Prometheus metric plugin on the Jenkins to Monitor the Jenkins Server

## Manage Jenkins -> Plugin search for Prometheus metrics installed it and restart the Jenkins.

![Screenshot 2024-02-06 155748](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/cbe53e23-a76f-4a4a-9eb9-fd093eae8140)

![Screenshot 2024-02-06 155929](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/8f1a5ca6-6bc2-40c7-afd3-3ef5ce194ff3)

## Edit the /etc/prometheus/prometheus.yml file

## sudo vim /etc/prometheus/prometheus.yml

```
 - job_name: "jenkins"
   static_configs:
     - targets: ["<jenkins-server-public-ip>:8080"]
```

```
 # my global config
 global:
  scrape_interval: 15s # Set the scrape interval to every 15 seconds. Default is every 1 minute.
  evaluation_interval: 15s # Evaluate rules every 15 seconds. The default is every 1 minute.
  # scrape_timeout is set to the global default (10s).

 # Alertmanager configuration
 alerting:
 alertmanagers:
    - static_configs:
        - targets:
          # - alertmanager:9093

 # Load rules once and periodically evaluate them according to the global 'evaluation_interval'.
 rule_files:
 # - "first_rules.yml"
 # - "second_rules.yml"

 # A scrape configuration containing exactly one endpoint to scrape:
 # Here it's Prometheus itself.
 scrape_configs:
 # The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
  - job_name: "prometheus"

   # metrics_path defaults to '/metrics'
   # scheme defaults to 'http'.

    static_configs:
     - targets: ["localhost:9090"]

 - job_name: "node_exporter"
   static_configs:
     - targets: ["localhost:9100"]

 - job_name: "jenkins"
   static_configs:
     - targets: ["3.95.160.167:8080"]
```

## Validated the prometheus config file

```
promtool check config /etc/prometheus/prometheus.yml

sudo systemctl restart prometheus.service
sudo systemctl status prometheus
```

![Screenshot 2024-02-06 172522](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/0ec6f851-3664-4f1e-8ca6-509b59c2f05b)

## Copied the public IP of the Monitoring Server and paste on the browser with a 9090 port with /targets.
## **http://3.83.224.209:9090/targets**

![Screenshot 2024-02-06 172843](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/aa82c30b-5b5b-4d77-8c3a-b2c609ea9ae3)

## Added Jenkins Dashboard on grafana server
## select New and Import
## Provide the 9964 to Load the dashboard and Load.
![image](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/232bff81-e412-4bbd-bc23-ca19df77bc92)

## Selected the default Prometheus from the drop-down menu and click on Import.

![Screenshot 2024-02-06 183841](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/8f5de659-1749-467f-821c-d959953f6185)

## integrated Email Alert. So, if our Jenkins pipeline will succeed or fail we will get a notification alert on our email.

## To do that, installed the Jenkins Plugin, whose name is Email Extension Template.

## After installing the plugin, an apps password was generated under security section of my email id through the Manage Account with jenkins as the app name and a password.

## Manage Jenkins -> Plugins and install the Email Extension Template plugin.

## configured the mail for the alerts.

## Go to Jenkins -> Manage Jenkins -> System

## Search for Extend E-mail Notification.

## Provided the smtp.gmail.com in the SMTP server and 465 in the SMTP port.

![Screenshot 2024-02-06 194947](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/86e4b51b-b954-4a6d-b933-ff7a65aa992e)

## Then, On the same page Search for Extend E-mail Notification.

## Provided the smtp.gmail.com in the SMTP server and 465 in the SMTP port.

## Selected Use SMTP Authentication and provide the Gmail ID and its password in the Username and password.

## To validate whether Jenkins can send the emails to you or not, check the Test configuration by sending a test e-mail.

![Screenshot 2024-02-06 195923](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/82b600ec-f10b-4a85-ace2-b44462d63a66)

![Screenshot 2024-02-06 201320](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/b04597bc-c8f4-40fb-a90d-0312ee9c6b62)


## set up the Jenkins Pipeline. But there are some plugins required to work with them.

## Downloaded the following plugins

## Eclipse Temurin installer

## SonarQube Scanner

## NodeJS

![Screenshot 2024-02-06 202329](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/807359c8-66bd-4a6a-9af8-8df90f275460)

## Configured the plugins

## Go to Manage Jenkins -> Tools

## Click on Add JDK and provide the following things below

![Screenshot 2024-02-06 204146](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/5be7f094-a6e7-4ceb-b95f-d62a61afad95)

![Screenshot 2024-02-06 204842](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/cb650260-95e8-4972-8a09-ed1696e4df2a)

## configured Sonarqube

## To access the sonarqube, copied the Jenkins Server public IP with port number 9000

## Then, click Security and click on Users.

## Clicked on the highlighted blue box on the right to generate the token.






























        

























