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

## 1.1  created a user called Test-user On the AWS Console and gave an administrator access permission. Access keys and secret access keys were then generated
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
## connected to the Jenkins Server
## 1.6 Installed python3
## **sudo apt install python3 -y**

![Screenshot 2024-02-26 010844](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/9a14071d-d238-4f54-bd9a-45f4cc438941)


## next, installed java
## **sudo apt-get install default-jdk -y**

![Screenshot 2024-02-26 011115](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/2114d781-e500-4a1a-8ba7-7637372f7530)

![Screenshot 2024-02-26 011158](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/a411965f-1c8b-4b17-812f-ddea4b5b4f4b)

![Screenshot 2024-02-26 011300](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/60b05559-1847-46ff-aee9-77b18d2f970d)


## 1.7 Installed Jenkins
```
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
/usr/share/keyrings/jenkins-keyring.asc > /dev/null

  echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt update -y

sudo apt-get install jenkins -y

service jenkins start

jenkins –version

```

![Screenshot 2024-02-26 011740](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/1f2d8a09-2fe7-4057-a547-a70b04b94634)

![Screenshot 2024-02-26 011920](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/7a8c8948-b150-450b-bcaf-ffe3294d3c1c)

## Step 2: Access Jenkins application
## 2.1	Open new browser and access Jenkins application deployed on a cloud instance with credentials as below:
## **34.204.69.175:8080**

![Screenshot 2024-02-26 012703](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/83e7cfce-6052-4de8-934b-2c079dda9539)

![Screenshot 2024-02-26 012824](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/eff6fe7c-e0bf-4031-97ac-a623af7f02d9)

## 2.2 Install Docker on the Jenkins server

```
sudo apt update

sudo apt install apt-transport-https ca-certificates curl software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update

apt-cache policy docker-ce

sudo apt install docker-ce

sudo usermod -aG docker jenkins

sudo systemctl start docker

systemctl status docker
```

## 2.3 Installed trivy for Image scanning

```
sudo apt-get install wget apt-transport-https gnupg lsb-release
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | sudo apt-key add -
echo deb https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main | sudo tee -a /etc/apt/sources.list.d/trivy.list
sudo apt-get update
sudo apt-get install trivy
```

![Screenshot 2024-02-26 013231](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/64d8d958-16d2-40d4-8b8e-793964304bce)

## Step 3: Created Jenkins pipeline to perform CI CD for a Docker container
## 3.1 Access Jenkins application and click on New Item to create a new Jenkins job: 
## 3.2 Selected desired Jenkins pipeline job type and fill in job name as per project requirement: 

![Screenshot 2024-02-26 013903](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/618abb6d-72e6-420c-8d1a-2f1edd5334d8)

## 3.3 Fork the GitHub Repository to configure Jenkins pipeline location.

## https://github.com/adeluyemi79/InsuranceManagement

## 3.4 navigated to Manage Jenkins  Manage Credentials and then select global domain. 

![Screenshot 2024-02-26 020351](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/b424942b-1b81-4c3d-a504-aa447248d5fd)

## 3.4 Clicked on new Credential by clicking on Add Credentials to create a new Docker hub credentials as per below details: 

![Screenshot 2024-02-26 021313](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/3e3d41c8-8fad-461b-8f28-ef1975f476d0)

## 3.5 Next provided full access to Docker Sock file using below command:
## chmod 777 /var/run/docker.sock

## Step 4: Execute Jenkins Build
 
## 4.1 Navigated to Jenkins job created and click on Build now to start running build for Jenkins job created.

![Screenshot 2024-02-26 040940](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/e10f162c-96d2-4e59-b727-68278137af39)

## 4.2 validated if Docker image really gets uploaded to Docker hub or not.

![Screenshot 2024-02-26 041218](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/b4809049-43e8-4b63-9670-762367aa2e15)

```
Started by user Adeyemi Adelu
Obtained Jenkinsfile from git https://github.com/adeluyemi79/InsuranceManagement
[Pipeline] Start of Pipeline
[Pipeline] node
Running on Jenkins in /var/lib/jenkins/workspace/Insurance-Pipeline
[Pipeline] {
[Pipeline] stage
[Pipeline] { (Prepare Environment)
[Pipeline] echo
Initialize Environment
[Pipeline] tool
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Code Checkout)
[Pipeline] checkout
Selected Git installation does not exist. Using Default
The recommended git tool is: NONE
No credentials specified
 > git rev-parse --resolve-git-dir /var/lib/jenkins/workspace/Insurance-Pipeline/.git # timeout=10
Fetching changes from the remote Git repository
 > git config remote.origin.url https://github.com/adeluyemi79/InsuranceManagement # timeout=10
Fetching upstream changes from https://github.com/adeluyemi79/InsuranceManagement
 > git --version # timeout=10
 > git --version # 'git version 2.34.1'
 > git fetch --tags --force --progress -- https://github.com/adeluyemi79/InsuranceManagement +refs/heads/*:refs/remotes/origin/* # timeout=10
 > git rev-parse refs/remotes/origin/master^{commit} # timeout=10
Checking out Revision d3b246e3d05c9177bf9d77d2c81bf382ccf17d89 (refs/remotes/origin/master)
 > git config core.sparsecheckout # timeout=10
 > git checkout -f d3b246e3d05c9177bf9d77d2c81bf382ccf17d89 # timeout=10
Commit message: "Update Jenkinsfile"
First time build. Skipping changelog.
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Maven Build)
[Pipeline] sh
+ /var/lib/jenkins/tools/hudson.tasks.Maven_MavenInstallation/maven/bin/mvn clean package
[INFO] Scanning for projects...
[INFO] 
[INFO] ------------------< com.project.insurance:insure-me >-------------------
[INFO] Building Insure-me 1.0
[INFO]   from pom.xml
[INFO] --------------------------------[ jar ]---------------------------------
[INFO] 
[INFO] --- clean:3.2.0:clean (default-clean) @ insure-me ---
[INFO] Deleting /var/lib/jenkins/workspace/Insurance-Pipeline/target
[INFO] 
[INFO] --- resources:3.2.0:resources (default-resources) @ insure-me ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] Using 'UTF-8' encoding to copy filtered properties files.
[INFO] Copying 1 resource
[INFO] Copying 31 resources
[INFO] 
[INFO] --- compiler:3.10.1:compile (default-compile) @ insure-me ---
[INFO] Changes detected - recompiling the module!
[INFO] Compiling 5 source files to /var/lib/jenkins/workspace/Insurance-Pipeline/target/classes
[INFO] 
[INFO] --- resources:3.2.0:testResources (default-testResources) @ insure-me ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] Using 'UTF-8' encoding to copy filtered properties files.
[INFO] skip non existing resourceDirectory /var/lib/jenkins/workspace/Insurance-Pipeline/src/test/resources
[INFO] 
[INFO] --- compiler:3.10.1:testCompile (default-testCompile) @ insure-me ---
[INFO] Changes detected - recompiling the module!
[INFO] Compiling 1 source file to /var/lib/jenkins/workspace/Insurance-Pipeline/target/test-classes
[INFO] 
[INFO] --- surefire:2.22.2:test (default-test) @ insure-me ---
[INFO] 
[INFO] -------------------------------------------------------
[INFO]  T E S T S
[INFO] -------------------------------------------------------
[INFO] Running com.project.insurance.insureme.InsureMeApplicationTests
09:08:48.599 [main] DEBUG org.springframework.test.context.BootstrapUtils - Instantiating CacheAwareContextLoaderDelegate from class [org.springframework.test.context.cache.DefaultCacheAwareContextLoaderDelegate]
09:08:48.609 [main] DEBUG org.springframework.test.context.BootstrapUtils - Instantiating BootstrapContext using constructor [public org.springframework.test.context.support.DefaultBootstrapContext(java.lang.Class,org.springframework.test.context.CacheAwareContextLoaderDelegate)]
09:08:48.646 [main] DEBUG org.springframework.test.context.BootstrapUtils - Instantiating TestContextBootstrapper for test class [com.project.insurance.insureme.InsureMeApplicationTests] from class [org.springframework.boot.test.context.SpringBootTestContextBootstrapper]
09:08:48.661 [main] INFO org.springframework.boot.test.context.SpringBootTestContextBootstrapper - Neither @ContextConfiguration nor @ContextHierarchy found for test class [com.project.insurance.insureme.InsureMeApplicationTests], using SpringBootContextLoader
09:08:48.665 [main] DEBUG org.springframework.test.context.support.AbstractContextLoader - Did not detect default resource location for test class [com.project.insurance.insureme.InsureMeApplicationTests]: class path resource [com/project/insurance/insureme/InsureMeApplicationTests-context.xml] does not exist
09:08:48.666 [main] DEBUG org.springframework.test.context.support.AbstractContextLoader - Did not detect default resource location for test class [com.project.insurance.insureme.InsureMeApplicationTests]: class path resource [com/project/insurance/insureme/InsureMeApplicationTestsContext.groovy] does not exist
09:08:48.666 [main] INFO org.springframework.test.context.support.AbstractContextLoader - Could not detect default resource locations for test class [com.project.insurance.insureme.InsureMeApplicationTests]: no resource found for suffixes {-context.xml, Context.groovy}.
09:08:48.667 [main] INFO org.springframework.test.context.support.AnnotationConfigContextLoaderUtils - Could not detect default configuration classes for test class [com.project.insurance.insureme.InsureMeApplicationTests]: InsureMeApplicationTests does not declare any static, non-private, non-final, nested classes annotated with @Configuration.
09:08:48.710 [main] DEBUG org.springframework.test.context.support.ActiveProfilesUtils - Could not find an 'annotation declaring class' for annotation type [org.springframework.test.context.ActiveProfiles] and class [com.project.insurance.insureme.InsureMeApplicationTests]
09:08:48.789 [main] DEBUG org.springframework.context.annotation.ClassPathScanningCandidateComponentProvider - Identified candidate component class: file [/var/lib/jenkins/workspace/Insurance-Pipeline/target/classes/com/project/insurance/insureme/InsureMeApplication.class]
09:08:48.815 [main] INFO org.springframework.boot.test.context.SpringBootTestContextBootstrapper - Found @SpringBootConfiguration com.project.insurance.insureme.InsureMeApplication for test class com.project.insurance.insureme.InsureMeApplicationTests
09:08:48.959 [main] DEBUG org.springframework.boot.test.context.SpringBootTestContextBootstrapper - @TestExecutionListeners is not present for class [com.project.insurance.insureme.InsureMeApplicationTests]: using defaults.
09:08:48.959 [main] INFO org.springframework.boot.test.context.SpringBootTestContextBootstrapper - Loaded default TestExecutionListener class names from location [META-INF/spring.factories]: [org.springframework.boot.test.mock.mockito.MockitoTestExecutionListener, org.springframework.boot.test.mock.mockito.ResetMocksTestExecutionListener, org.springframework.boot.test.autoconfigure.restdocs.RestDocsTestExecutionListener, org.springframework.boot.test.autoconfigure.web.client.MockRestServiceServerResetTestExecutionListener, org.springframework.boot.test.autoconfigure.web.servlet.MockMvcPrintOnlyOnFailureTestExecutionListener, org.springframework.boot.test.autoconfigure.web.servlet.WebDriverTestExecutionListener, org.springframework.boot.test.autoconfigure.webservices.client.MockWebServiceServerTestExecutionListener, org.springframework.test.context.web.ServletTestExecutionListener, org.springframework.test.context.support.DirtiesContextBeforeModesTestExecutionListener, org.springframework.test.context.event.ApplicationEventsTestExecutionListener, org.springframework.test.context.support.DependencyInjectionTestExecutionListener, org.springframework.test.context.support.DirtiesContextTestExecutionListener, org.springframework.test.context.transaction.TransactionalTestExecutionListener, org.springframework.test.context.jdbc.SqlScriptsTestExecutionListener, org.springframework.test.context.event.EventPublishingTestExecutionListener]
09:08:48.979 [main] INFO org.springframework.boot.test.context.SpringBootTestContextBootstrapper - Using TestExecutionListeners: [org.springframework.test.context.web.ServletTestExecutionListener@4ddbbdf8, org.springframework.test.context.support.DirtiesContextBeforeModesTestExecutionListener@3f67593e, org.springframework.test.context.event.ApplicationEventsTestExecutionListener@1ab06251, org.springframework.boot.test.mock.mockito.MockitoTestExecutionListener@41ab013, org.springframework.boot.test.autoconfigure.SpringBootDependencyInjectionTestExecutionListener@14bee915, org.springframework.test.context.support.DirtiesContextTestExecutionListener@1115ec15, org.springframework.test.context.transaction.TransactionalTestExecutionListener@82ea68c, org.springframework.test.context.jdbc.SqlScriptsTestExecutionListener@59e505b2, org.springframework.test.context.event.EventPublishingTestExecutionListener@3af0a9da, org.springframework.boot.test.mock.mockito.ResetMocksTestExecutionListener@43b9fd5, org.springframework.boot.test.autoconfigure.restdocs.RestDocsTestExecutionListener@79dc5318, org.springframework.boot.test.autoconfigure.web.client.MockRestServiceServerResetTestExecutionListener@8e50104, org.springframework.boot.test.autoconfigure.web.servlet.MockMvcPrintOnlyOnFailureTestExecutionListener@37e4d7bb, org.springframework.boot.test.autoconfigure.web.servlet.WebDriverTestExecutionListener@6f7923a5, org.springframework.boot.test.autoconfigure.webservices.client.MockWebServiceServerTestExecutionListener@74a6f9c1]
09:08:48.982 [main] DEBUG org.springframework.test.context.support.AbstractDirtiesContextTestExecutionListener - Before test class: context [DefaultTestContext@69f1a286 testClass = InsureMeApplicationTests, testInstance = [null], testMethod = [null], testException = [null], mergedContextConfiguration = [WebMergedContextConfiguration@7922d892 testClass = InsureMeApplicationTests, locations = '{}', classes = '{class com.project.insurance.insureme.InsureMeApplication}', contextInitializerClasses = '[]', activeProfiles = '{}', propertySourceLocations = '{}', propertySourceProperties = '{org.springframework.boot.test.context.SpringBootTestContextBootstrapper=true}', contextCustomizers = set[org.springframework.boot.test.context.filter.ExcludeFilterContextCustomizer@5fa07e12, org.springframework.boot.test.json.DuplicateJsonObjectContextCustomizerFactory$DuplicateJsonObjectContextCustomizer@1649b0e6, org.springframework.boot.test.mock.mockito.MockitoContextCustomizer@0, org.springframework.boot.test.web.client.TestRestTemplateContextCustomizer@65f095f8, org.springframework.boot.test.autoconfigure.actuate.metrics.MetricsExportContextCustomizerFactory$DisableMetricExportContextCustomizer@e7edb54, org.springframework.boot.test.autoconfigure.properties.PropertyMappingContextCustomizer@0, org.springframework.boot.test.autoconfigure.web.servlet.WebDriverContextCustomizerFactory$Customizer@34f5090e, org.springframework.boot.test.context.SpringBootTestArgs@1, org.springframework.boot.test.context.SpringBootTestWebEnvironment@9660f4e], resourceBasePath = 'src/main/webapp', contextLoader = 'org.springframework.boot.test.context.SpringBootContextLoader', parent = [null]], attributes = map['org.springframework.test.context.web.ServletTestExecutionListener.activateListener' -> true]], class annotated with @DirtiesContext [false] with mode [null].

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::                (v2.7.4)

2024-02-26 09:08:49.397  INFO 15360 --- [           main] c.p.i.insureme.InsureMeApplicationTests  : Starting InsureMeApplicationTests using Java 11.0.21 on ip-172-31-90-24 with PID 15360 (started by jenkins in /var/lib/jenkins/workspace/Insurance-Pipeline)
2024-02-26 09:08:49.402  INFO 15360 --- [           main] c.p.i.insureme.InsureMeApplicationTests  : No active profile set, falling back to 1 default profile: "default"
2024-02-26 09:08:50.368  INFO 15360 --- [           main] .s.d.r.c.RepositoryConfigurationDelegate : Bootstrapping Spring Data JPA repositories in DEFAULT mode.
2024-02-26 09:08:50.422  INFO 15360 --- [           main] .s.d.r.c.RepositoryConfigurationDelegate : Finished Spring Data repository scanning in 46 ms. Found 1 JPA repository interfaces.
2024-02-26 09:08:51.128  INFO 15360 --- [           main] com.zaxxer.hikari.HikariDataSource       : HikariPool-1 - Starting...
2024-02-26 09:08:51.349  INFO 15360 --- [           main] com.zaxxer.hikari.HikariDataSource       : HikariPool-1 - Start completed.
2024-02-26 09:08:51.414  INFO 15360 --- [           main] o.hibernate.jpa.internal.util.LogHelper  : HHH000204: Processing PersistenceUnitInfo [name: default]
2024-02-26 09:08:51.495  INFO 15360 --- [           main] org.hibernate.Version                    : HHH000412: Hibernate ORM core version 5.6.11.Final
2024-02-26 09:08:51.688  INFO 15360 --- [           main] o.hibernate.annotations.common.Version   : HCANN000001: Hibernate Commons Annotations {5.1.2.Final}
2024-02-26 09:08:51.816  INFO 15360 --- [           main] org.hibernate.dialect.Dialect            : HHH000400: Using dialect: org.hibernate.dialect.H2Dialect
2024-02-26 09:08:52.451  INFO 15360 --- [           main] o.h.e.t.j.p.i.JtaPlatformInitiator       : HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
2024-02-26 09:08:52.461  INFO 15360 --- [           main] j.LocalContainerEntityManagerFactoryBean : Initialized JPA EntityManagerFactory for persistence unit 'default'
2024-02-26 09:08:53.069  WARN 15360 --- [           main] JpaBaseConfiguration$JpaWebConfiguration : spring.jpa.open-in-view is enabled by default. Therefore, database queries may be performed during view rendering. Explicitly configure spring.jpa.open-in-view to disable this warning
2024-02-26 09:08:53.384  INFO 15360 --- [           main] o.s.b.a.w.s.WelcomePageHandlerMapping    : Adding welcome page: class path resource [static/index.html]
2024-02-26 09:08:53.713  INFO 15360 --- [           main] c.p.i.insureme.InsureMeApplicationTests  : Started InsureMeApplicationTests in 4.692 seconds (JVM running for 6.041)
[INFO] Tests run: 3, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 5.395 s - in com.project.insurance.insureme.InsureMeApplicationTests
2024-02-26 09:08:53.945  INFO 15360 --- [ionShutdownHook] j.LocalContainerEntityManagerFactoryBean : Closing JPA EntityManagerFactory for persistence unit 'default'
2024-02-26 09:08:53.946  INFO 15360 --- [ionShutdownHook] .SchemaDropperImpl$DelayedDropActionImpl : HHH000477: Starting delayed evictData of schema as part of SessionFactory shut-down'
2024-02-26 09:08:53.958  INFO 15360 --- [ionShutdownHook] com.zaxxer.hikari.HikariDataSource       : HikariPool-1 - Shutdown initiated...
2024-02-26 09:08:53.972  INFO 15360 --- [ionShutdownHook] com.zaxxer.hikari.HikariDataSource       : HikariPool-1 - Shutdown completed.
[INFO] 
[INFO] Results:
[INFO] 
[INFO] Tests run: 3, Failures: 0, Errors: 0, Skipped: 0
[INFO] 
[INFO] 
[INFO] --- jar:3.2.2:jar (default-jar) @ insure-me ---
[INFO] Building jar: /var/lib/jenkins/workspace/Insurance-Pipeline/target/insure-me-1.0.jar
[INFO] 
[INFO] --- spring-boot:2.7.4:repackage (repackage) @ insure-me ---
[INFO] Replacing main artifact with repackaged archive
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  10.869 s
[INFO] Finished at: 2024-02-26T09:08:55Z
[INFO] ------------------------------------------------------------------------
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Publish Test Reports)
[Pipeline] publishHTML
[htmlpublisher] Archiving HTML reports...
[htmlpublisher] Archiving at PROJECT level /var/lib/jenkins/workspace/Insurance-Pipeline/target/surefire-reports to /var/lib/jenkins/jobs/Insurance-Pipeline/htmlreports/HTML_20Report
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Docker Image Build)
[Pipeline] echo
Creating Docker image
[Pipeline] sh
+ docker build -t adeluyemi79/insure-me:3.0 --pull --no-cache .
#0 building with "default" instance using docker driver

#1 [internal] load build definition from Dockerfile
#1 transferring dockerfile: 142B done
#1 DONE 0.0s

#2 [internal] load metadata for docker.io/library/openjdk:11
#2 DONE 0.1s

#3 [internal] load .dockerignore
#3 transferring context: 2B done
#3 DONE 0.0s

#4 [1/2] FROM docker.io/library/openjdk:11@sha256:99bac5bf83633e3c7399aed725c8415e7b569b54e03e4599e580fc9cdb7c21ab
#4 CACHED

#5 [internal] load build context
#5 transferring context: 40.48MB 0.4s done
#5 DONE 0.4s

#6 [2/2] COPY target/*.jar app.jar
#6 DONE 1.0s

#7 exporting to image
#7 exporting layers
#7 exporting layers 0.2s done
#7 writing image sha256:ffc3547cd057263e864f5a27cc4ccceb58cb8f8e24358cfb60aea95a70e38f14 done
#7 naming to docker.io/adeluyemi79/insure-me:3.0 done
#7 DONE 0.2s
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Docker Image Scan)
[Pipeline] echo
Scanning Docker image for vulnerbilities
[Pipeline] sh
+ docker build -t adeluyemi79/insure-me:3.0 .
#0 building with "default" instance using docker driver

#1 [internal] load build definition from Dockerfile
#1 transferring dockerfile: 142B done
#1 DONE 0.0s

#2 [internal] load metadata for docker.io/library/openjdk:11
#2 DONE 0.0s

#3 [internal] load .dockerignore
#3 transferring context: 2B done
#3 DONE 0.0s

#4 [internal] load build context
#4 transferring context: 74B done
#4 DONE 0.0s

#5 [1/2] FROM docker.io/library/openjdk:11
#5 CACHED

#6 [2/2] COPY target/*.jar app.jar
#6 DONE 0.2s

#7 exporting to image
#7 exporting layers
#7 exporting layers 0.2s done
#7 writing image sha256:b958ce6475954b2e5a96a11faf632f6cbd54da036f9ae94644b233a13eac9c8a done
#7 naming to docker.io/adeluyemi79/insure-me:3.0 done
#7 DONE 0.2s
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Publishing Image to DockerHub)
[Pipeline] echo
Pushing the docker image to DockerHub
[Pipeline] withCredentials
Masking supported pattern matches of $dockerPassword
[Pipeline] {
[Pipeline] sh
Warning: A secret was passed to "sh" using Groovy String interpolation, which is insecure.
		 Affected argument(s) used the following variable(s): [dockerPassword]
		 See https://jenkins.io/redirect/groovy-string-interpolation for details.
+ docker login -u adeluyemi79 -p ****
WARNING! Using --password via the CLI is insecure. Use --password-stdin.
WARNING! Your password will be stored unencrypted in /var/lib/jenkins/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded
[Pipeline] sh
+ docker push adeluyemi79/insure-me:3.0
The push refers to repository [docker.io/adeluyemi79/insure-me]
bb9a8a2012e3: Preparing
7b7f3078e1db: Preparing
826c3ddbb29c: Preparing
b626401ef603: Preparing
9b55156abf26: Preparing
293d5db30c9f: Preparing
03127cdb479b: Preparing
9c742cd6c7a5: Preparing
293d5db30c9f: Waiting
03127cdb479b: Waiting
9c742cd6c7a5: Waiting
826c3ddbb29c: Mounted from library/openjdk
9b55156abf26: Mounted from library/openjdk
7b7f3078e1db: Mounted from library/openjdk
b626401ef603: Mounted from library/openjdk
293d5db30c9f: Mounted from library/openjdk
03127cdb479b: Mounted from library/openjdk
9c742cd6c7a5: Mounted from library/openjdk
bb9a8a2012e3: Pushed
3.0: digest: sha256:c3d7cd289c0110bf859eb0bae53d012e2088f44e5ad5b0742c096a56ffe1055c size: 2007
[Pipeline] echo
Image push complete
[Pipeline] }
[Pipeline] // withCredentials
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Docker Container Deployment)
[Pipeline] sh
+ docker rm insure-me -f
Error response from daemon: No such container: insure-me
[Pipeline] sh
+ docker pull adeluyemi79/insure-me:3.0
3.0: Pulling from adeluyemi79/insure-me
Digest: sha256:c3d7cd289c0110bf859eb0bae53d012e2088f44e5ad5b0742c096a56ffe1055c
Status: Image is up to date for adeluyemi79/insure-me:3.0
docker.io/adeluyemi79/insure-me:3.0
[Pipeline] sh
+ docker run -d --rm -p 8081:8081 --name insure-me adeluyemi79/insure-me:3.0
a9934af7a39f58a0ef125febba5804df6b3e51613cc3e17572788f5676e80872
[Pipeline] echo
Application started on port: 8081 (http)
[Pipeline] }
[Pipeline] // stage
[Pipeline] }
[Pipeline] // node
[Pipeline] End of Pipeline
Finished: SUCCESS
```

## Step 5: Access Deployed application on Docker container
 
## 5.1 After the Docker container has been deployed The server IP address and port 8081 was use to access application.

# **34.204.69.175:8081**


![Screenshot 2024-02-26 042339](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/e088904d-e16e-4437-b2a6-9f378c03235f)

![Screenshot 2024-02-26 042403](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/6eea77c7-cb27-41ae-8a6f-78b57ea9ffac)

![Screenshot 2024-02-26 042426](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/d7f73a48-e1d6-4fb2-b751-5bb1873c5834)

![Screenshot 2024-02-26 042459](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/80b3ff80-10d1-484c-aba7-51cc13444a87)

![Screenshot 2024-02-26 042527](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/f499dfa7-c975-4f5a-9b09-d8b00204574c)

![Screenshot 2024-02-26 042540](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/770241b5-f50b-4422-b9ef-2e3d8d567446)


























