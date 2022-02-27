# DOCK IMAGE
```powershell
# GET EXISTING DOCKER IAMGES
% docker search Ubuntu

# 1. download specific version of ubuntu file
% docker pull ubuntu:16.04 

# 2. CHECK LOCAL IMAGE
# check all images locally 
% docker image ls -a
# docker image ls <string>
% docker image ls ubuntu 

# REMOVE IMAGE
# docker image rm <imageID>
% docker image rm fb6

# GIVE IMAGE A NAME 
% docker tag <imageID> <imageName>:<imageVersion>
% docker tag fb6 mydockerimage:1.0
```
# DOCK CONTAINER
```powershell
# 3. CREATE CONTAINER FOR EXISTING IMAGE
# docker run -it <imageID> <shell system>
% docker run -it 657 bash
    # -i: interactive interface 
    # –t: terminal
    # Bash: Unix shell and command language
    # 657 is the first 3 numbers in the image ID. 

# EXIT FROM ROOT CONTAINERS
% exit

# 4. CHECK ALL CONTAINERS
% docker container ls -a

# EXPORT CONTAINER
# docker export <containerID> -o <name.tar> 
% docker export fb6 -o mycontainer.tar  

# REMOVE CONTAINER
# docker container rm <containerID>
% docker container rm fb6

# IMPORT CONTAINER TO SYSTEM
# docker import <name.tar> 
% docker import mycontainer.tar  

# RUN EXISTING CONTAINER OR RESTART CONTAINER
# docker container start <containerID>
% docker container start a9d
% docker exec -it a9d bash 
```
# DOCKER FILE
```powershell
DOCKER FILE --> DOCKER HUB --> BUIld
# Create new file named Dockerfile with below code under working directory
% vim Dockerfile
    FROM ubuntu:16.04
    WORKDIR ./
    RUN mkdir mydockerfile

# BUILD THE DOCKER FILE 
% docker build .

# NAME THE DOCKER FILE 
% docker tag fb6 mydockerimage:1.0

% vim Dockerfile
    FROM ubuntu:16.04
    RUN apt-get update && apt-get install -y \
    apt-transport-https \
    python3 \
    python3-pip \
    && pip3 install --upgrade pip \ && rm -rf /var/lib/apt/lists/*
    #set the working directory for containers
    WORKDIR /usr/src/House_Price
    # Copy all the files from the project’s root to the working
    COPY $path /usr/src/House_Price/
    RUN ls -la /usr/src/House_Price/*
    # Installing python dependencies
    RUN pip3 install --no-cache-dir -r 
    /usr/src/House_Price/requirements.txt

# BUILD THE DOCKER FILE 
# docker build -t <name:versionID> --build-arg path="<PATH>" .
% docker build -t hp_model:1.0 --build-arg path="C:/Users/Ke/Downloads/Docker/House_Price/" .
```
# PUSH DOCKER TO HUB 
```powershell
1. login in on https://hub.docker.com/ 
2. create Repository 
3. RUN
% docker login --username=<your user name>
# docker tag <imageID> <usrname>/<dockerfilename>:<versionID>
% docker tag 61d mialu/mydocker:1.0
% docker push 61d mialu/mydocker:1.0
```
# OTHER ACTIONS 
```powershell
---------------OTHER ACTIONS---------------
# CHECK CONTAINER AND IMAGE SIZE
% docker system df
```

# SOURCE 
* [Docker - 从入门到实践](https://yeasy.gitbook.io/docker_practice/)

* [Docker Docs](https://docs.docker.com/)