---
title: SpringBoot+travis-ci+Github+Docker+Docker-compose+Watchower实现自动化部署更新
date: 2020/10/28 14:47:15
categories: SpringBoot
tags:
    - SpringBoot
    - 其他
cover_picture: https://i.loli.net/2020/06/02/tFQRdryksBI1uvL.png
---

## SpringBoot+travis-ci+Github+Docker+Docker-compose实现自动化部署

<!-- more -->

自动部署可以实现开发过程中,我只需要将代码推送至git仓库,会有软件帮我自动完成打包部署的操作.

### 需要

1. 一台centos服务器

2. 注册[travis-ci](https://travis-ci.com/)的账号

3. 注册Github账号

4. 注册Docker账号

### SpringBoot

项目采用SpringBoot框架

#### Dockerfile

在SpringBoot项目的根路径下面创建一个名为`Dockerfile`的文件,文件类型也选择Dokerfile

Dockerfile作为打包Docker镜像时的配置文件

Dockerfile的内容如下:

```dockerfile
## 指定所需依赖的基础镜像
FROM adoptopenjdk/openjdk11:alpine
## VOLUME 指向了一个/tmp的目录，由于 Spring Boot 使用内置的Tomcat容器，Tomcat 默认使用/tmp作为工作目录。这个命令的效果是：在宿主机的/var/lib/docker目录下创建一个临时文件并把它链接到容器中的/tmp目录
VOLUME /tmp
## 将当前目录下的jar包复制到docker容器的根目录下
## target/course-0.0.1-SNAPSHOT.jar 项目打包成的jar包位于target文件夹下
ADD target/course-0.0.1-SNAPSHOT.jar app.jar
## 声明服务运行在8080端口
EXPOSE 8080
## 指定docker容器启动时运行jar包
ENTRYPOINT ["nohup","java","-jar","/app.jar" ]
```

### travis-ci

travis-ci是一个免费提供ci的网站,创建账号并与Github的账号绑定

首先在travis-ci中新建以一个仓库并与github上的仓库绑定

#### .travis.yml

在SpringBoot项目的根路径下面创建一个名为`.travis`的yml文件

此文件内容主要是travis-ci自动打包代码，并打包成Docker镜像的配置文件

```yml
## 语言为Java
language: java
## 需不需要管理员权限
sudo: required
## 选择的分支
branches:
  only:
    - main
## 所用的jdk文件
jdk:
  - openjdk11
services:
- docker
before_install:
  - chmod +x ./mvnw
script:
## 打包的命令
  - mvn clean package -Dmaven.test.skip=true
## 登录Docker的命令，此处的DOCKER_PASSWORD以及DOCKER_USERNAME是在travis的项目中配置的环境变量
  - echo "$DOCKER_PASSWORD" |  docker login -u "$DOCKER_USERNAME" --password-stdin
## 构建镜像
  - docker image build ./ -t xdqingyuan/course-server:latest
## 发布镜像
  - docker image push xdqingyuan/course-server:latest
```

[设置环境变量的教程](https://docs.travis-ci.com/user/environment-variables/)

### Centos服务器配置

首先在服务器中安装Docker以及docker-compose

```shell
yum install docker

yum install docker-compose
```

#### 新建一个文件夹作为项目根路径


在文件夹中新建一个名为`docker-compose.yml`的文件

```yml
version: '3'
services:
 course:
  image: xdqingyuan/course-server:latest
  restart: always
  ports:
    - 8080:8080
  volumes:
  #将docker-compose.yml的文件夹映射到docker容器的a-course文件夹
    - ./:/a-course
  container_name: course
```

查看日志输出

```shell
docker-compose logs service-name
```

#### 指定日志输出路径

```yml
logging:
  file:
  #此处./a-course/代表Docker容器根路径下的a-course文件夹
    name: ./a-course/course.log
```

在Springboot的配置文件中增加如下配置,指定输出到/a-course/course.log文件中，并通过docker-compose.yml的配置将/a-course/数据卷挂载到宿主机的/a-course/文件

#### 启动项目

```shell
docker-compose up -d
```

#### 查看docker容器配置

```
docker inspect container-name
```

查看数据卷是否挂载成功

![docker-a-course.png](https://i.loli.net/2020/10/30/gHAliJEOjxuDM6o.png)

#### 查看docker容器中的文件

```shell
docker exec container-name ls file-name
```

![docker-ls.png](https://i.loli.net/2020/10/30/7jK6fWA9I2oGlC8.png)

#### 集成watchower实现自动化更新

在上述的docker-compose.yml文件中添加如下内容

```yml
version: '3'
services:
 course:
  image: xdqingyuan/course-server:latest
  restart: always
  ports:
    - 8080:8080
  volumes:
    - ./:/a-course
  container_name: course
##配置watchower自动更新
 watchtower:
  image: containrrr/watchtower
  volumes:
   - /var/run/docker.sock:/var/run/docker.sock
  # course指定容器名称
  # --interval 30 30秒检查一次更新
  #  --cleanup 清除之前的镜像
  command: course  --cleanup  --interval 30
  container_name: watchower
```

随后无需再手动执行 `docker stop course`等命令,手动更新镜像和容器.

### 总结

Dockerfile

```dockerfile
## 指定所需依赖的基础镜像
FROM adoptopenjdk/openjdk11:alpine
## VOLUME 指向了一个/tmp的目录，由于 Spring Boot 使用内置的Tomcat容器，Tomcat 默认使用/tmp作为工作目录。这个命令的效果是：在宿主机的/var/lib/docker目录下创建一个临时文件并把它链接到容器中的/tmp目录
VOLUME /tmp
## 将当前目录下的jar包复制到docker容器的/a-course目录下
## 若不存在该目录Docker会自动创建该目录
ADD target/course-0.0.1-SNAPSHOT.jar app.jar
## 声明服务运行在8080端口
EXPOSE 8080
## 指定docker容器启动时运行jar包 并指定日志输出到
ENTRYPOINT ["nohup","java","-jar","/app.jar" ]
```

.travis.yml

```yml
language: java
sudo: required
branches:
  only:
    - main
jdk:
  - openjdk11
services:
- docker
before_install:
  - chmod +x ./mvnw
script:
  - mvn clean package -Dmaven.test.skip=true
  - echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin
  - docker image build ./ -t xdqingyuan/course-server:latest
  - docker image push xdqingyuan/course-server:latest
```

docker--compose.yml

```yml
version: '3'
services:
 course:
  image: xdqingyuan/course-server:latest
  restart: always
  ports:
    - 8080:8080
  volumes:
    - ./:/a-course
  container_name: course
 watchtower:
  image: containrrr/watchtower
  volumes:
   - /var/run/docker.sock:/var/run/docker.sock
  # 30秒检查一次更新
  command: course  --cleanup  --interval 30
  container_name: watchower
```