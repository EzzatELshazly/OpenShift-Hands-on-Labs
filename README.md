# OpenShift-Hands-on-Labs

## Introduction
OpenShift is a comprehensive and robust container application platform developed by Red Hat, built on top of Kubernetes. It provides a range of tools and services to help developers and IT operations teams build, deploy, and manage containerized applications.

<p align="center"><img src="screenshots/OpenShift-Logo.png" width="20%" height="20%">
<br><em>OpenShift logo</em>
</p>


## Prerequisite 
### 1. Have access to openshift cluster. 
### 2. Install openshift on your linux virtual machine. 

#### Install OpenShift on Ubuntu
**- Update system by using following commands**
```shell
$ sudo apt update
$ sudo apt upgrade
```
**- Install docker**
```shell
$ sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
**- Start the docker service and enable it**
```shell
$ sudo systemctl start docker
$ sudo systemctl enable docker
```
**- Check the status of docker service**
```shell
$ sudo systemctl status docker
```
**- Install OpenShift origin**
```shell
$ sudo wget https://github.com/openshift/origin/releases/download/v3.11.0/openshift-origin-client-tools-v3.11.0-0cbc58b-linux-64bit.tar.gz
```
**- Once it is downloaded successfuly untar (extract) the file**
```shell
$ sudo tar -xvzf openshift-origin-client-tools-v3.11.0-0cbc58b-linux-64bit.tar.gz
```
**- change directory to the extracted file**
```shell
$ cd openshift-origin-client-tools-v3.11.0-0cbc58b-linux-64bit
```
**- copy oc and kubectl to /usr/local/bin and check the version**
```shell
$ sudo cp oc kubectl /usr/local/bin/
$ oc version
```
**- The result should be in the image bellow**
<p align="center"><img src="screenshots/oc version.PNG" width="50%" height="50%">
<br><em>oc version result</em> 
</p>

**- Access your openshift cluster via Terminal (oc command-line tool)**
```shell
$ oc login https://"link of the oc cluster":"Port" -u "your username" -p "your Password"
```

## 1st lab: Deployment and rollback 
### Objectives
* Deploy NGINX with 3 replicas.
* Create a service to expose NGINX deployment. 
* Use port forwarding to access NGINX service locally. 
* Update the deployment to use Apache image insted of Nginx image.
* View deployment's rollout history. 
* Roll back NGINX deployment to the previous image (Nginx) and Monitor pod status to confirm successful rollback.


### 1. Spring Boot Application Deployment Using Jenkins on OpenShift

The objective of automating the deployment of a Spring Boot application within an OpenShift cluster is achieved through Jenkins. By developing Jenkins pipelines that efficiently manage the deployment lifecycle from code commit to production deployment, we ensure a scalable and resilient process. 


### 2. AWS Infrastructure Provisioning Using Terraform

Provision and manage a complete AWS infrastructure using Terraform, enabling IaC practices. This approach not only streamlines the creation of AWS resources but also integrates them with CloudWatch for monitoring and alerting.

**Deploying the terraform modules to provision resources:**
* Install AWS CLI and add your AWS user access key and secret access key to enable

```shell
$ curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
$ unzip awscliv2.zip
$ sudo ./aws/install
$ aws configure
```
> [!NOTE]
> To test,verify and run your terraform code. 

```shell
$ terraform init
$ terraform plan
$ terraform apply
```

<p align="center"><img src="screenshots/terraform/terraform tree last.png" width="50%" height="50%">
<br><em>Terraform structure</em> 
</p>

<p align="center"><img src="screenshots/terraform/final terraform.png" width="90%" height="90%">
<br><em>Terraform apply results</em> 
</p>

### 3. EC2 Instance Configuration Using Ansible
Utilizing Ansible for configuring AWS EC2 instances to host services such as Git, Docker, Java, Jenkins, SonarQube, and OpenShift. This approach ensures consistent and repeatable setups across instances, leading to fully configured and operational EC2 instances ready to support various stages of the DevOps pipeline.
1. Create a key pair on AWS. Download it to be used in the dynamic inventory and change its permissions as follows:
```shell
$ chmod 400 IvolveKey.pem
```
2. Run the ansible playbook using the following command
```shell
$ ansible-playbook -i inventory/aws_ec2.yml ec2.yml
```
<p align="center"><img src="screenshots/Ansible/ansible structure.png" width="90%" height="90%">
<br><em>Ansible structure</em> 
</p>

<p align="center"><img src="screenshots/Ansible/asnible playbook amazon linux run.png" width="90%" height="90%">
<br><em>Ansible-playbook results on Ec2</em> 
</p>

<p align="center"><img src="screenshots/Ansible/ansible playbook in the local inventory.png" width="90%" height="90%">
<br><em>Ansible-playbook results on local machines</em> 
</p>

<p align="center"><img src="screenshots/Ansible/connect to ec2.png" width="90%" height="90%">
<br><em>Connect to your Ec2</em> 
</p>


you can access you sonarqube by writing yourIp:9000

> [!NOTE]
> You can not run sonarqube in ec2 t2.micro instance. you need a t2.large.

<p align="center"><img src="screenshots/Ansible/sonarqube login.png" width="90%" height="90%">
<br><em>SonarQube login</em> 
</p>

<p align="center"><img src="screenshots/Ansible/create local project sonar.png" width="90%" height="90%">
<br><em>Create SonarQube project</em> 
</p>

### 4. Centralized Monitoring and Logging with OpenShift
Implemented a centralized monitoring and logging system within the OpenShift cluster as we mentioned in the instructions provided in the reposistory in the instructions folder(Instructions/Instructions-for-setup-for-centralized-loggingTask8.docx). We gain insights into application performance and overall cluster health, thus enhancing operational visibility and intelligence.

### 5. Containerization of the Java Application

Containerizing the Java application is a key part of this project, ensuring environment consistency and ease of deployment. The development of a Dockerfile, detailing all dependencies and configurations, leads to a containerized version of the Java application. 
> [!NOTE]
> Before building the image you need to: chmod +x gradlew

To build your image run the following command

```shell
$ sudo docker build -t nameOfYourApp:tag .
```

To run your image run the following command on a specific port

```shell
$ sudo docker run -d -p 8081:8080 (for example) nameOfYourApp:tag 
```
> [!NOTE]
> Note if the port does not run try to add this port in the firewall


To check your running containers

```shell
$ sudo docker ps
```

<p align="center"><img src="screenshots/docker/docker build .png" width="90%" height="90%">
<br><em>Docker build results</em> 
</p>

<p align="center"><img src="screenshots/docker/docker image run localhost 8081.png" width="90%" height="90%">
<br><em>Accessing Application </em> 
</p>

### 6. CI/CD Automation with Jenkins

Automate the CI/CD process using Jenkins, thereby streamlining the application deployment lifecycle. The development of a Jenkins pipeline script integrates various stages, including code build, testing, and deployment. This results in a seamless, automated pipeline that accelerates the release cycle and reduces manual intervention.

> [!NOTE]
> You need to add your credentials (dockerhub, github, openshift and sonarqube)

<p align="center"><img src="screenshots/jenkins/credentials.png" width="90%" height="90%">
<br><em>Jenkins credentials</em> 
</p>

<p align="center"><img src="screenshots/jenkins/jenkins final pipeline run.png" width="90%" height="90%">
<br><em>Success Pipeline</em> 
</p>

<p align="center"><img src="screenshots/jenkins/test.png" width="90%" height="90%">
<br><em>Unit Test</em> 
</p>

<p align="center"><img src="screenshots/jenkins/pushed to dockerhub.png" width="90%" height="90%">
<br><em>Jenkins compile Pushing to docker hub</em> 
</p>

<p align="center"><img src="screenshots/jenkins/push to docker hub final.png" width="90%" height="90%">
<br><em>Build and Push to docker hub</em> 
</p>

<p align="center"><img src="screenshots/jenkins/deploy to openshift.png" width="90%" height="90%">
<br><em>Deploy to openshift and create the resources </em> 
</p>

<p align="center"><img src="screenshots/jenkins/Deployments.png" width="90%" height="90%">
<br><em>Deployment in the openshift cluster</em> 
</p>

<p align="center"><img src="screenshots/jenkins/Service.png" width="90%" height="90%">
<br><em>Service created </em> 
</p>

<p align="center"><img src="screenshots/jenkins/Route.png" width="90%" height="90%">
<br><em>Route created </em> 
</p>

<p align="center"><img src="screenshots/jenkins/access application.png" width="90%" height="90%">
<br><em>Accessing the Application using route</em> 
</p>

### 7. Jenkins Shared Library
This repository houses a comprehensive Jenkins Shared Library designed to elevate your Continuous Integration and Continuous Deployment (CI/CD) workflows. By centralizing reusable Groovy scripts, this library aims to simplify pipeline definition, enhance code reusability, and streamline your Jenkins pipeline development.

> [!NOTE]
> Before running your shared library you need some configurations. check on allow default > version to be overridden and include @library changes in job recent changes.

<p align="center"><img src="screenshots/jenkins/global shared library.png" width="90%" height="90%">
<br><em>Global Pipeline Libraries</em> 
</p>

> [!NOTE]
> Add your GitHub Repo,credentials and your vars path in the library path 

<p align="center"><img src="screenshots/jenkins/shared library config.png" width="90%" height="90%">
<br><em>Global Pipeline Libraries</em> 
</p>

## Conclusion
