# Welcome to my DevOps-SDLC-Project ☁️🙋‍

## Explanation of Project: 
In this project, the deployment of a web application to a production server is being done following the Software Development Life Cycle and utilizing DevOps tools. The first step in this process is using a Terraform script to build AWS EC2 instances. This is a more efficient method compared to building the backend on the AWS console, as it can be automated and saves time and effort.

Once the EC2 instances are ready, Jenkins is configured on an EC2 Medium server, and a CICD pipeline is built. This is achieved by configuring Sonarqube for checking code standards and Nexus artifact repository for taking backups. The configuration is done on individual EC2 instances to ensure scalability and fault tolerance.

Apache Tomcat is then configured on the production server where the web application is to be deployed. This ensures that the server is ready to handle the application once it is deployed.

For monitoring the production server, Prometheus is configured along with the Nord exporter, which uses Grafana dashboard for real-time monitoring. This provides updates on the performance of the web application in real-time, allowing for timely troubleshooting of issues.

To monitor the logs of the production server where the application is deployed, ElasticSearch and Metricbeats are configured. This allows for easy access to logs and enables quick identification and resolution of any problems that may arise.

Finally, Nginx is used as a reverse proxy to hide the IP address of the production server on which the application is running. This provides an additional layer of security and helps keep the server safe from any malicious attacks.

In conclusion, this project takes a comprehensive approach to deploying a web application on a production server, utilizing a wide range of DevOps tools to ensure efficient deployment, effective monitoring, and high-level security. The use of DevOps tools ensures that the deployment process is streamlined, and issues can be quickly identified and resolved.









# System Architecture Design:
![image](https://user-images.githubusercontent.com/64432661/232321563-e7fba5a6-3540-410b-a8f3-5275ce03387b.png)

## Terraform:
I written the below terraform script to create the backend infrastructure on AWS, which will be required for configuring sonarqube and nexus repo. Using Infrastructure-as-Code is much more efficient instead of building the backend on the AWS console.
<img width="1100" alt="Screenshot 2023-04-17 at 1 24 14 PM" src="https://user-images.githubusercontent.com/64432661/232577131-ffc1e4da-8689-4908-b761-32246f1a82cf.png">
Here i have written a script that would install a Aapche Tomcat on one the first ec2 instance, which will be used as a production server on which the application will be deployed.
<img width="795" alt="terraform 2023-04-17 at 1 47 38 PM" src="https://user-images.githubusercontent.com/64432661/232582342-2338151f-3bf9-4bfa-8541-554bbbcc66da.png">

## Jenkins:
I have configured jenkins on t2.medium (always use t2.medium or higher for Jenkins, because t2.micro's hardware is insufficient for jenkins and it would crash). 
I have set up Jenkins as an application rather than a service. As Jenkins is an application, it needs Tomcat to be installed in order to function. Here i have used declartive script for this pipeline. 

<img width="1160" alt="Screenshot 2023-04-17 at 2 13 34 PM" src="https://user-images.githubusercontent.com/64432661/232587841-5bc8c488-3ad6-48e3-a873-f111afb7baf8.png">

This can also be done using freestyle pipleline we have to install sonarqube and nexus plugins for this to work.
 
<img width="418" alt="Screenshot 2023-04-17 at 2 16 28 PM" src="https://user-images.githubusercontent.com/64432661/232588491-eaa7c169-c6ce-4f2f-b231-2c4263b73621.png">

### Installing SonarQube:
I have configured sonarQube on Ubuntu server, below are the list of commands i have used:
```bash
sudo apt install wget
```
```bash
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-5.6.7.zip
```
