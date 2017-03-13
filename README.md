# Dockerfile for tomcat9jdk8
Tomcat9(9.0.0.M17) with Oracle jdk8(8u121)

[![Docker Hub](https://img.shields.io/docker/pulls/zzjhacn/tomcat9jdk8.svg?style=flat)](https://registry.hub.docker.com/u/zzjhacn/tomcat9jdk8/)
[![Docker Hub](https://img.shields.io/docker/stars/zzjhacn/tomcat9jdk8.svg?style=flat)](https://registry.hub.docker.com/u/zzjhacn/tomcat9jdk8/)

**Dockerfiles** for [Tomcat9](https://tomcat.apache.org) with [Oracle Java 8](http://www.oracle.com/technetwork/java/index.html) on [Alpine](https://registry.hub.docker.com/_/alpine/) for Docker Automated/Trusted Builds.

**Using the image, you accept the [Oracle Binary Code License Agreement](http://www.oracle.com/technetwork/java/javase/terms/license/index.html) for Java SE and [Apache License version 2](http://www.apache.org/licenses) for tomcat.**

[![](https://img.shields.io/badge/size-78MB-blue.svg)]() zzjhacn/tomcat9jdk8

```
docker run -d --privileged=true --restart always \
  -p 8880:8080 \
  -v /opt/apps/app_1/tomcat_conf:/tomcat/conf \
  -v /opt/apps/app_1/tomcat_log:/usr/local/tomcat/logs \
  -v /opt/apps/app_1/app:/usr/local/tomcat/webapps \
  --name tomcat9 zzjhacn/tomcat9jdk8
```
