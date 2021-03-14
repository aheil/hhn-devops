# Docker Layer 

In this lab you will learn basic principles about layers in Docker. To goal of this lab is to enable you to optimize the size of your Docker images. 

## Lab Exercise

Each Docker image consists of a set of layers where the lower layers are read-only layers while the topmost layer is a readable/writeable layer.

Each layer is called *intermediate image*.

1. Create a file called `helloworld.sh`. 
2. Edit the file:

    ```bash
    #!/bin/bash
    echo "Hello World!" 
    ```
    **Excursion**  
    The signs at the firs line are called *sha-bang* or *she-bang*, based on the signs sharp (#) and bang (!). If a script starts with a she-bank, the first line of the file is parsed and the directive is used as the interpreter to be executed and the rest of the script is send to the interpreter defined in the first line. 

3. Create a file called `Dockerfile`.
4. Edit the file:

    ```docker
    FROM alpine
    COPY helloworld.sh /helloworld.sh 
    CMD [ "bash", "helloworld.sh"]
    ```

5. Run `docker build .`

    ```bash
    > docker build .
    Sending build context to Docker daemon  3.072kB
    Step 1/3 : FROM alpine
    latest: Pulling from library/alpine
    188c0c94c7c5: Pull complete
    Digest: sha256:c0e9560cda118f9ec63ddefb4a173a2b2a0347082d7dff7dc14272e7841a5b5a
    Status: Downloaded newer image for alpine:latest
     ---> d6e46aa2470d
    Step 2/3 : COPY helloworld.sh /helloworld.sh
     ---> 22bce47fdc17
    Step 3/3 : CMD [ "bash", "helloworld.sh"]
     ---> Running in 8f1c16adb870
    Removing intermediate container 8f1c16adb870
     ---> 59b55d71dfdf
    Successfully built 59b55d71dfdf
    ```  
    
    The command above caused Docker to build a new image based on the `Dockerfile` in the current folder.

6. Re-run the build using `docker build -t lab02`.

    ```bash
    > docker build -t lab02 .
    Sending build context to Docker daemon  3.072kB
    Step 1/3 : FROM alpine
     ---> d6e46aa2470d
    Step 2/3 : COPY helloworld.sh /helloworld.sh
     ---> Using cache
     ---> 22bce47fdc17
    Step 3/3 : CMD [ "bash", "helloworld.sh"]
     ---> Using cache
     ---> 59b55d71dfdf
    Successfully built 59b55d71dfdf
    Successfully tagged lab02:latest
    ```

    Using this command, you tagged the latest build. Eventually, you see, that docker used its cache to build the image. 

    Each command in your `Dockerfile` causes Docker to create a new intermediate image which potentially could be reused. Each layer can be identified by its randomly generated ID. 

7. Start your container calling `docker run lab02`

    By now, you should run into an error, as you image is missing an important component, the bash-Shell (aka Bourne-again shell), which is the most common used shell in UNIX/Linux systems.

8. Change the `Dockerfile` by adding a line for installing the package containing the bash-shell.

    ```Docker
    FROM alpine
    RUN apk add bash
    COPY helloworld.sh /helloworld.sh 
    CMD [ "bash", "helloworld.sh"]
    ```

9. Rerun `docker build -t lab02`.

    ```shell
    > docker build -t lab02 .
    Sending build context to Docker daemon  3.072kB
    Step 1/4 : FROM alpine
     ---> d6e46aa2470d
    Step 2/4 : RUN apk add bash
     ---> Running in 3e10379a4857
    fetch http://dl-cdn.alpinelinux.org/alpine/v3.12/main/x86_64/APKINDEX.tar.gz
    fetch http://dl-cdn.alpinelinux.org/alpine/v3.12/community/x86_64/APKINDEX.tar.gz
    (1/4) Installing ncurses-terminfo-base (6.2_p20200523-r0)
    (2/4) Installing ncurses-libs (6.2_p20200523-r0)
    (3/4) Installing readline (8.0.4-r0)
    (4/4) Installing bash (5.0.17-r0)
    Executing bash-5.0.17-r0.post-install
    Executing busybox-1.31.1-r19.trigger
    OK: 8 MiB in 18 packages
    Removing intermediate container 3e10379a4857
     ---> c3b8be85b888
    Step 3/4 : COPY helloworld.sh /helloworld.sh
     ---> f256f29276b9
    Step 4/4 : CMD [ "bash", "helloworld.sh"]
     ---> Running in 13f4f21ec6cb
    Removing intermediate container 13f4f21ec6cb
     ---> c16c26d5b9ad
    Successfully built c16c26d5b9ad
    Successfully tagged lab02:latest
    ```

10. Now run `docker run lab02` again:

    ```bash
    > docker run lab02
    Hello World!
    ```

11. To investigate the build steps of your image run ``docker history lab02`. 

    ```bash
    > docker history lab02
    IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
    3fcd2278e94f        12 minutes ago      /bin/sh -c #(nop)  CMD ["bash" "helloworld.s…   0B
    f256f29276b9        15 minutes ago      /bin/sh -c #(nop) COPY file:cde93dfb7de260dc…   32B
    c3b8be85b888        15 minutes ago      /bin/sh -c apk add bash                         3.79MB
    d6e46aa2470d        2 weeks ago         /bin/sh -c #(nop)  CMD ["/bin/sh"]              0B
    <missing>           2 weeks ago         /bin/sh -c #(nop) ADD file:f17f65714f703db90…   5.57MB
    ```

    **Exkursion:**  
    For each step in your `Dockerfile`, you will find the corresponding intermediate image listed here. While Docker runs a Shell for every layer, each line which does not start with `RUN` is commented by `#(nop)` (no operations). Every command that is not `RUN` command must not be interpreted by the shell and is treated by Docker internally. Read your `Dockerfile`one more time and rethink what you have just read. This makes a lot of sense, as wach command not starting with `RUN` in the Dockerfile starts with a special keyword.

## Conclusion 

You now have created a new docker image with multiple layers. 

By following this lab you might already get an idea how to reduce the size of your images. 

1. Reduce the numbers of layers by using multi-line commands

    ```Docker
    ...
    apt-get update
    apt-get install bash 
    at-get install openssl 
    apt-get install jq 
    apt-get install git
    ...  
    ```
    
    should be written 

    ```Docker
    apt-get update && apt-get install -y \\
        update \
        openssl \
        jq \
        get \
    ...
    ```
    instead.  

2. Use optimal base images, try to avoid large base images with unnecessary components in it. 

3. Only install, copy and add files and packages you need in your image. 

4. Use `docker history` to find commands causing a new layer to be created. Avoid unnecessary commands. You can use [dive](https://github.com/wagoodman/dive) to inspect your layers to find unnecessary layers.  

5. No application data in images. 

6.  Once you optimized layers, consider to build your own custom base image.

7. Use [multi-stage builds](https://docs.docker.com/develop/develop-images/multistage-build/) (not covered in this lab) to reduce the image size.

---
v1.0.0

Last modified: 2020/11/10 20:54:56