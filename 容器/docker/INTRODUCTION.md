# Docker入门
## Docker是什么
Docker是一个开源的应用容器引擎，基于Go语言并遵从Apache2.0协议开源。Docker可以让开发者打包他们的应用以及依赖包到一个轻量级、可移植
的容器中。容器是完全沙箱机制，相互之间不会有任何接口，最重要的是容器性能开销很低。

---

## Docker基本概念
	Docker中三个非常重要的概念
	1. Image(镜像)：Docker镜像就相当于一个root文件系统。
	2. Container(容器): Image和Container的关系类似于面向对象程序设计中的类和实例一样，镜像是静态的定义，容器是镜像运行的实体。
	3. Respository(仓库)：用来保存镜像的仓库。

---	

## Docker实践
### 镜像使用
当容器运行时，使用的镜像如果在本地不存在，docker就是自动从docker镜像仓库中下载，默认是从Docker Hub公共镜像源下载。

#### 1.列出镜像列表
docker images
<div>
    <img src="../../img/images1.png"  width="60%" height="60%">
</div> 

选项说明:  
+ REPOSITORY:表示镜像的仓库源  
+ TAG：镜像的标签  
+ IMAGE ID：镜像ID  
+ SIZE：镜像大小

#### 2.查找镜像
docker search
<div>
	<img src="../../img/images2.png" width="60%" height="60%">
</div>  

+ NAME: 镜像仓库名称
+ DESCIPTION：镜像描述
+ OFFICIAL：是否docker官方发布
+ stars：类似Github中的star
+ AUTOMATED：自动构建

#### 3.获取一个新镜像
docker pull

#### 4.删除镜像
docker rmi 

#### 5. 创建镜像
当从docker镜像仓库中下载的镜像不能满足需求时，可以通过下面两种方式对镜像进行更改。  
1. 从已经创建的镜像容器中更新镜像，并且提交这个镜像；  
2. 使用Dockerfile指令来创建一个镜像。

---

### 容器使用
#### 1. 启动容器
docker run -it ubuntu /bin/bash  
参数说明：  
- i:交互操作
- t:终端
- ubuntu:镜像
- /bin/bash:命令，得到交互的shell

#### 2. 停止容器
docker stop <容器 ID>

#### 3. 启动已停止容器  
docker restart <容器 ID>

#### 4. 后台运行
docker run -itd --name ubuntu-test ubuntu /bin/bash

#### 5. 进入容器
- docker attach(退出会导致容器停止)
- docker exec（退出不会影响容器）

#### 6. 导出和导入容器
- export
- import
#### 7. 删除容器
docker rm -f 容器ID

---

### 容器链接
容器中可以运行一些网络应用，要让外部也可以访问这些应用，可以通过-P或-p参数来指定端口映射。
#### 1. 网络端口映射
- -P是容器内部端口随机映射到主机的高端口
- -p是容器内部端口绑定到指定的主机端口

#### 2. 容器互联
#### 3. 配置DNS

---

### 仓库管理

---

### Dockerfile
Dockerfile是一个用来构建镜像的文本文件，文本内容包含了一条条构建镜像所需的指令和说明。

---

### Compose
Compose 是用于定义和运行多容器 Docker 应用程序的工具。通过 Compose，您可以使用 YML 文件来配置应用程序需要的所有服务。然后，使用一个命令，就可以从 YML 文件配置中创建并启动所有服务

---

### Machine

---

### Swarm集群管理

---

## 附录
Docker官网：<https://www.docker.com>  
Github Docker源码：<https://github.com/docker/docker-ce>  
镜像加速：<http://hub-mirror.c.163.com>


