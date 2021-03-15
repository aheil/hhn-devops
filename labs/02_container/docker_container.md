# Lab: Docker Container 

In this lab, you will create a docker image providing a basic web server. 

## Tasks

* Create a `Dockerfile` to be used to build your Docker image.
* Install nginx within the Docker image. 
* Make sure to provide a default site for the nginx server.
* Create a volume (bind mount) to provide a index.html via your hosts file system.
* Expose port 80 within the Docker image.
* Make sure the nginx server starts when the container based on your image started.


**Remark: Do not use the official NGINX docker image, make sure to install nginx instead using your own Dockerfile.**
