## Docker

* Features
1) Containerization Platform
2) Better than VMs as it consumes less resources
3) Easily shareable and can be used to replucate whole envs.

```sh
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/codebuild-repo$ sudo su
[sudo] password for ravi0531rp: 
root@ravi-MSI:/home/ravi0531rp/Desktop/CODES/u-miscellaneous/codebuild-repo# docker image ls
REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
hello-world   latest    d2c94e258dcb   9 months ago   13.3kB
root@ravi-MSI:/home/ravi0531rp/Desktop/CODES/u-miscellaneous/codebuild-repo# docker ps -a
CONTAINER ID   IMAGE         COMMAND    CREATED      STATUS                  PORTS     NAMES
ed645119b04e   hello-world   "/hello"   8 days ago   Exited (0) 8 days ago             eager_nash
root@ravi-MSI:/home/ravi0531rp/Desktop/CODES/u-miscellaneous/codebuild-repo# docker --version
Docker version 25.0.1, build 29cf629
root@ravi-MSI:/home/ravi0531rp/Desktop/CODES/u-miscellaneous/codebuild-repo# docker run hello-world

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/

root@ravi-MSI:/home/ravi0531rp/Desktop/CODES/u-miscellaneous/codebuild-repo# docker pull busybox
Using default tag: latest
latest: Pulling from library/busybox
9ad63333ebc9: Pull complete 
Digest: sha256:6d9ac9237a84afe1516540f40a0fafdc86859b2141954b4d643af7066d598b74
Status: Downloaded newer image for busybox:latest
docker.io/library/busybox:latest
root@ravi-MSI:/home/ravi0531rp/Desktop/CODES/u-miscellaneous/codebuild-repo# docker image ls
REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
busybox       latest    3f57d9401f8d   2 weeks ago    4.26MB
hello-world   latest    d2c94e258dcb   9 months ago   13.3kB
root@ravi-MSI:/home/ravi0531rp/Desktop/CODES/u-miscellaneous/codebuild-repo# docker run busybox
root@ravi-MSI:/home/ravi0531rp/Desktop/CODES/u-miscellaneous/codebuild-repo# docker run 3f57d9401f8d
root@ravi-MSI:/home/ravi0531rp/Desktop/CODES/u-miscellaneous/codebuild-repo# docker run 3f57d9401f8d echo "hello from busybox"
hello from busybox
root@ravi-MSI:/home/ravi0531rp/Desktop/CODES/u-miscellaneous/codebuild-repo# docker ps -a
CONTAINER ID   IMAGE          COMMAND                  CREATED              STATUS                          PORTS     NAMES
2f31c38a3a4f   3f57d9401f8d   "echo 'hello from bu…"   20 seconds ago       Exited (0) 20 seconds ago                 confident_mclean
c3708a70cd71   3f57d9401f8d   "sh"                     49 seconds ago       Exited (0) 48 seconds ago                 great_heyrovsky
bb67db67f80b   busybox        "sh"                     About a minute ago   Exited (0) About a minute ago             angry_dhawan
0c19e38b2202   hello-world    "/hello"                 About a minute ago   Exited (0) About a minute ago             boring_williams
ed645119b04e   hello-world    "/hello"                 8 days ago           Exited (0) 8 days ago                     eager_nash
root@ravi-MSI:/home/ravi0531rp/Desktop/CODES/u-miscellaneous/codebuild-repo# docker run -it busybox sh
/ # ls
bin    dev    etc    home   lib    lib64  proc   root   sys    tmp    usr    var
/ # pwd
/
/ # uptime
 21:03:11 up 3 days,  6:03,  0 users,  load average: 0.77, 0.92, 0.91
/ # exit
root@ravi-MSI:/home/ravi0531rp/Desktop/CODES/u-miscellaneous/codebuild-repo# docker rm 2f31c38a3a4f
2f31c38a3a4f
root@ravi-MSI:/home/ravi0531rp/Desktop/CODES/u-miscellaneous/codebuild-repo# docker ps -a
CONTAINER ID   IMAGE          COMMAND    CREATED          STATUS                      PORTS     NAMES
84ce99d87825   busybox        "sh"       10 minutes ago   Exited (0) 4 minutes ago              jovial_brown
c3708a70cd71   3f57d9401f8d   "sh"       11 minutes ago   Exited (0) 11 minutes ago             great_heyrovsky
bb67db67f80b   busybox        "sh"       12 minutes ago   Exited (0) 12 minutes ago             angry_dhawan
0c19e38b2202   hello-world    "/hello"   12 minutes ago   Exited (0) 12 minutes ago             boring_williams
ed645119b04e   hello-world    "/hello"   8 days ago       Exited (0) 8 days ago                 eager_nash
root@ravi-MSI:/home/ravi0531rp/Desktop/CODES/u-miscellaneous/codebuild-repo# 



```

* Building images and running Containers

```sh
docker build -t ravi0531rp/docker-app-flask:latest .


```

* Push them to ECR
1) Create a repo on ECR
2) Go to View Push commands

```sh
root@ravi-MSI:/home/ravi0531rp/Desktop/CODES/u-miscellaneous/docker-app-flask# aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 992219819011.dkr.ecr.us-east-1.amazonaws.com

Unable to locate credentials. You can configure credentials by running "aws configure".
Error: Cannot perform an interactive login from a non TTY device
root@ravi-MSI:/home/ravi0531rp/Desktop/CODES/u-miscellaneous/docker-app-flask# aws configure
AWS Access Key ID [None]: AKIA6OBHI5QBXGWWLL32
AWS Secret Access Key [None]: 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
Default region name [None]: us-east-1
Default output format [None]: json
root@ravi-MSI:/home/ravi0531rp/Desktop/CODES/u-miscellaneous/docker-app-flask# aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 992219819011.dkr.ecr.us-east-1.amazonaws.com
WARNING! Your password will be stored unencrypted in /root/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded
root@ravi-MSI:/home/ravi0531rp/Desktop/CODES/u-miscellaneous/docker-app-flask# docker build -t ravi0531/docker-app-flask .
[+] Building 2.1s (9/9) FINISHED                                                                                                                                                            docker:default
 => [internal] load build definition from Dockerfile                                                                                                                                                  0.0s
 => => transferring dockerfile: 339B                                                                                                                                                                  0.0s
 => [internal] load metadata for docker.io/library/python:3.8                                                                                                                                         2.1s
 => [internal] load .dockerignore                                                                                                                                                                     0.0s
 => => transferring context: 2B                                                                                                                                                                       0.0s
 => [1/4] FROM docker.io/library/python:3.8@sha256:84783b524e4227352f0a3a23520c7e717d5a5b9cff7d7fe174be54ae113b57f0                                                                                   0.0s
 => [internal] load build context                                                                                                                                                                     0.0s
 => => transferring context: 191B                                                                                                                                                                     0.0s
 => CACHED [2/4] WORKDIR /usr/src/app                                                                                                                                                                 0.0s
 => CACHED [3/4] COPY . .                                                                                                                                                                             0.0s
 => CACHED [4/4] RUN pip install --no-cache-dir -r requirements.txt                                                                                                                                   0.0s
 => exporting to image                                                                                                                                                                                0.0s
 => => exporting layers                                                                                                                                                                               0.0s
 => => writing image sha256:683ac694aae76645bc5fdfc34a7ad8b2ab99d000bf8823afc7c208e546cf5423                                                                                                          0.0s
 => => naming to docker.io/ravi0531/docker-app-flask                                                                                                                                                  0.0s
root@ravi-MSI:/home/ravi0531rp/Desktop/CODES/u-miscellaneous/docker-app-flask# docker tag ravi0531/docker-app-flask:latest 992219819011.dkr.ecr.us-east-1.amazonaws.com/ravi0531/docker-app-flask:latest
root@ravi-MSI:/home/ravi0531rp/Desktop/CODES/u-miscellaneous/docker-app-flask# docker push 992219819011.dkr.ecr.us-east-1.amazonaws.com/ravi0531/docker-app-flask:latest

```

* Using Codebuild for ECR
Now, we will use codebuild to generate an Image and push it to ECR

Dockerfile
```sh
FROM golang:1.12-alpine AS build
#Install git
RUN apk add --no-cache git
#Get the hello world package from a GitHub repository
RUN go get github.com/golang/example/hello
WORKDIR /go/src/github.com/golang/example/hello
# Build the project and send the output to /bin/HelloWorld 
RUN go build -o /bin/HelloWorld

FROM golang:1.12-alpine
#Copy the build's output binary from the previous build container
COPY --from=build /bin/HelloWorld /bin/HelloWorld
ENTRYPOINT ["/bin/HelloWorld"]

```

```sh
version: 0.2
#Test


phases:
  pre_build:
    commands:
      - echo Logging in to Amazon ECR...
      - aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 992219819011.dkr.ecr.ap-south-1.amazonaws.com
  build:
    commands:
      - echo Build started on `date`
      - echo Building the Docker image...          
      - docker build -t ecr-demo .
      - docker tag ecr-demo:latest 992219819011.dkr.ecr.ap-south-1.amazonaws.com/ecr-demo:latest
  post_build:
    commands:
      - echo Build completed on `date`
      - echo Pushing the Docker image...
      - docker push 992219819011.dkr.ecr.ap-south-1.amazonaws.com/ecr-demo:latest

```

* Then all steps as we had done..
Add sufficient access for ECR to the service role created for the Codebuild project. 