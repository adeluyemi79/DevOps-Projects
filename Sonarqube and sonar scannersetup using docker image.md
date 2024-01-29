# **Sonarqube and sonar scannersetup using docker image**

## **SonarQube** is an open-source platform developed for continuous inspection of code quality to perform automatic reviews with static analysis of code to detect bugs, code smells, and security vulnerabilities. It’s often used in the context of Continuous Integration and Continuous Deployment (CI/CD) pipelines to ensure that code quality is maintained throughout the development process.

## **SonarScanner** is a command-line tool provided by SonarQube. It is responsible for collecting information about your project and running the code analysis.

## **SonarQube** provides a centralized server for storing and processing code analysis results, while SonarScanner is a tool used by developers to perform the actual code analysis and send the results to the SonarQube server for further processing and reporting. Together, they enable continuous code quality monitoring and improvement.

## **Step 1**: Created a docker network to install the sonarqube and sonarscanner
## **docker network create sonar_network**

![Screenshot 2024-01-29 133600](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/ba8f0664-ae7b-41dc-bb5c-4d96433a22ca)

## **Step 2**: Run the below command to run the sonarqube image 
## **docker run -d --name sonarqube --network sonar_network -p 9000:9000 sonarqube**

![Screenshot 2024-01-29 134029](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/913fc3c6-a8b7-4557-9411-d4f86e602726)

## **Step 3**: Accessed the sonarqube server UI in the localhost: 9000, with default username and password admin.

![Screenshot 2024-01-29 134800](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/6363aaf8-6775-49c4-b486-b055e66ec30c)

![Screenshot 2024-01-29 135140](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/125d1b41-b41b-4bd7-a177-9dd48a51fc55)
## **Step 4**: Generated a token, go to my account → security → generate token, in that path you can generate a token.

![Screenshot 2024-01-29 140236](https://github.com/adeluyemi79/DevOps-Projects/assets/144259400/1182eccf-9513-4542-b09e-c8ea39e41b99)




