---
layout: post
title: Docker best practices
date:   2019-10-23 08:38:00 +0100
categories: [tools, docker]
tags: [programming, tools, docker]
---
List of things to do, to improve your Docker experience

### Never map the public port on a DockerFile  
If you map it, you'll only be able to have one instance of this container running. If the user wants to map the port, he'll be able to do it in a `compose` script or with `-p` option.
~~~ bash
# public and private mapping
EXPOSE 80:8080 # don't do this

# private mapping
EXPOSE 80
~~~

<!--more-->

### CMD and ENTRYPOINT better together  
The difference is `CMD` arguments may be overwritten while `ENTRYPOINT` may not.  
The best use of them is together, with `ENTRYPOINT` setting the main application to launch and `CMD` setting the _args_ or _flags_ for this application.  

~~~ bash
ENTRYPOINT ["bundle", "exec", "jekyll", "serve"]
CMD ["--host", "0.0.0.0"]
~~~

#### Give CMD (or ENTRYPOINT) an interactive shell  
In most other cases `CMD` should be given an interactive shell such as _python_ or _bash_. Using this form means, that when you execute something along the lines of `docker run -it python`, you'll get dropped into a usable shell.  

~~~ bash
CMD ["python"]
~~~

### Keep your images small  
#### Use .dockerignore
This excludes files not relevant to the build, without restrucuring your sources. It supports the same syntax as `.gitignore`.

#### Use the Cache
Try to always keep your _DockerFiles_ consistent. If they have the same parent image and the same commands' order (except `ADD`), it will hit the cache instead of executing them.  
Put all common instructions on top and all the changes at the bottom of your _DockerFile_.

#### Minimize the number of instructions
_(This is still important for Docker < 17.05. For newer versions, create a multistage build)_  
Each `RUN`, `COPY` and `ADD` instruction in a _DockerFile_ adds a layer to the image. It's a good practice to group them together with shell tricks to avoid unneded new layers.  

~~~ shell
# For example, is better to use just one RUN with && instead of two
RUN go get -d -v golang.org/x/net/html \
  && CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o app .
~~~

##### apt-get  
Avoid `RUN apt-get upgrade` and `dist-upgrade`. Many _essential_ packages cannot upgrade in a unpriviliged contaier.  

If you're going to do it, **always** combine `apt-get upgrade` with `apt-get install` in the same `RUN` statement. Otherwise it causes issues with Docker's image cache.  
Also, clean up _apt's_ cache when done.
~~~ bash
RUN apt-get update && apt-get install -y \
    package-bar \
    package-baz
    && rm -rf /var/lib/apt/lists/*
~~~

#### Use multistage builds  
_(This requires Docker > 17.05)_  
This tries to improve the bad maintainability at the previous point. Now it's possible to use one image as builder and after doing all the steps we need to get our item together, we can just copy it into a new image and deploy from there. Use it when possible  

One practical example for this would be building a Java App in a Maven image and then deploying in another Java-alpine or Tomcat image. This way we don't have all the dependencies for Maven at our final build.  

~~~ bash
# Build image - won't be included for release. Just compiles.
FROM maven:3.6.1-jdk-8-alpine AS builder
WORKDIR /usr/src/app
COPY app .
RUN mvn -f pom.xml clean package

# Deploy image
FROM openjdk:8u212-jre-alpine
COPY --from=builder /usr/src/app/target/my-java-app-*-SNAPSHOT.jar \
  /usr/src/myapp/my-java-app.jar
EXPOSE 8080
ENTRYPOINT ["java","-jar","/usr/src/myapp/my-java-app.jar"]
~~~

## Reference(s)
[http://crosbymichael.com/dockerfile-best-practices.html](http://crosbymichael.com/dockerfile-best-practices.html)  
[https://docs.docker.com/develop/dev-best-practices/](https://docs.docker.com/develop/dev-best-practices/)  
[https://docs.docker.com/develop/develop-images/multistage-build/](https://docs.docker.com/develop/develop-images/multistage-build/)  
[https://docs.docker.com/develop/develop-images/dockerfile_best-practices/](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)  
