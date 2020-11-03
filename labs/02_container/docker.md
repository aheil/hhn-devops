Exercise: Docker

In this exercise you create an image which could potentially be used as a runner in a CI/CD process.

Tasks: 
1. Create a `Dockerfile` file to be used to build your Docker  image.
2. Create a `docker.compose.yml` file to build your image and t start your container. 
3. Your image has to meet the following requirements:
    1. The image is automatically created when 'docker-compose up' is called. 
    2. If you start the container, the Git repository specified will be cloned within your container. The repository URL can be specified within the `docker-compose.yml`file. The repository URL must not be hard-coded in the image. 
    3. The container starts *Checkstyle* an performs and analysis of the code specified in the source code folder based on the *Google Java Style Guide*.
    4. The file containing the *Google Java Style Guide* is provided along with the  `Dockerfile` and can be changed prior to the creation of the image.
    5. The location of the source code within the given repository can be specified in the `docker-compose.yml`file. It must not be hard-coded within the image.
    6. The execution of *Checkstyle* within your container is  triggered by a  *Gradle* script.
    7. Both, the parameters for the source file as well as the repository URL can be changed in the 'docker-compose.yml'. The change will take effect after the next start of the container without the need or rebuilding the image.
    8. All errors occurring can be viewed in the container`s log. 
    9. If coding conventions specified by the *Google Java Style Guide* are not met, the output can be viewed in the container log as well.

---
v1.0.0

Last modified: 2020/11/02 09:34:07