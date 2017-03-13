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


working_dir : `exp: /opt/apps/app_1/`
* $working_dir/tomcat_conf: place configuration file(s) for tomcat
* $working_dir/tomcat_log: tomcat logs dir
* $working_dir/app: tomcat webapps dir

----

simple shell for initializing a app `sh Initializing.sh [app_name] [port]`

Initializing.sh
```shell
#!/bin/sh
[ -z "$1" ] && echo "Usage : $0 [app_name] [port]" && exit 1

port=9999
[ -n "$2" ] && port=$2

base_dir=/opt/apps/$1

echo "Initializing app[$1] with tomcat on port[$port]..."

mkdir -p $base_dir/tomcat_conf
mkdir -p $base_dir/tomcat_log
mkdir -p $base_dir/app
mkdir -p $base_dir/app/ROOT

echo "
docker run -d --privileged=true --restart always \\
  -p $port:8080 \\
  -v $base_dir/tomcat_conf:/tomcat/conf:Z \\
  -v $base_dir/tomcat_log:/usr/local/tomcat/logs:Z \\
  -v $base_dir/app:/usr/local/tomcat/webapps:Z \\
  --name $1 zzjhacn/tomcat9jdk8
" > $base_dir/dockerrun.sh

echo "
<!DOCTYPE html>
<html>
  <head>
    <meta charset='utf-8'>
    <title>Redirecting...</title>
    <meta http-equiv='refresh' content='0.2;url=/$1'>
    <script type='text/javascript'>
      window.location.href='/$1';
    </script>
  </head>
  <body>
    If web page not redirect to automatically, you can <a href='/$1'>click here</a> to go.
  </body>
</html>
" > $base_dir/app/ROOT/index.html

echo "Done!
You can run [ $base_dir/dockerrun.sh ] when place your war file into dir [ $base_dir/app/ ].
Docker container named[$1] will listen on local port $port.
"
```
