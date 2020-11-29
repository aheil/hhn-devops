# Lab 09 - Kubernetes 
## Exercise - Simple App Deployment 

In this exercise you will create an deployment where you apply various techniques and skills acquired during the previous lessons.

In this exercise you will deploy a web server in a docker image. 
You will provide a static web page, served by the web server running in the corresponding container. The container as well as the static web pages will be deployed in a Vagrantbox using an Ansible script. 


### Task 1 - Docker Image

1. Create a Docker image suitable for the above scenario. Choose the base image of any Linux distribution you want to use. 
2. Make sure either *nginx* od *apache* will be installed in the image. 
3. Make sure the static web page is provided via a volume to the container to be exchangeable.

### Task 2 - Vagrantbox 

4. Create a Vagrantbox capable of running docker and to be provisioned via Ansible. 
4. Create an Ansible script to deploy both, the image as well as the static web site content to your Vagrantbox.  


