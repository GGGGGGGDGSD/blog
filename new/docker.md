
## 安装

这个安装官网来没什么问题

1. docker工作原理
  client server 模式 守护进程在主机上运行 通过socket与客户端连接  接受client的指令响应

2. 常用命令
  docker info
  docker version
  docker --help
  docker ps 查看本地当前运行的容器
  docker images  查看本机上的镜像
  docker run -it ubuntu /bin/bash 启动一个ubuntu shell
  docker run -dp 80:80 docker/getting-started 启动示范demo
  docker exec -it 容器  进入正在运行的容器

## 镜像
1. 镜像的原理
   一层一层的文件组成的联合系统文件
- 查看本地镜像
  docker images

- 查找镜像
  以从 Docker Hub 网站来搜索镜像，Docker Hub 网址为： https://hub.docker.com/
  也可以用docker search name 搜索

- 拉取镜像
  docker pull <name>

- remove 
   docker rmi <name>

- 创建镜像(重点)
   创建一个 Dockerfile 文件  通过 docker build 命令来构建一个镜像

- docker commit 提交新的镜像
  这个就能解决我之前想持久化Ubuntu数据的问题

- docker build 构建镜像


## Docker Compose
  通过 Compose，您可以使用 YML 文件来配置应用程序需要的所有服务。然后，使用一个命令，就可以从 YML 文件配置中创建并启动所有服务

  - Compose 使用的三个步骤：
    使用 Dockerfile 定义应用程序的环境。

    使用 docker-compose.yml 定义构成应用程序的服务，这样它们可以在隔离环境中一起运行。

    最后，执行 docker-compose up 命令来启动并运行整个应用程序。

## 数据卷
docker run -it -v 主机目录：容器目录  挂载卷


## dockerfile
  用来构建镜像的文件
  docker build 构建镜像

  docker history 可以查看镜像的构建历史

  docker push  发布镜像
![nice][images/1.png]


## docker 网络


## 参考
- [Docker--从入门到实践](https://yeasy.gitbook.io/docker_practice/)
- [Docker Cheat Sheet](https://github.com/wsargent/docker-cheat-sheet#images)




## UT
- 基础组件单元测试
  a 表单类基础组件单元测试
  b 常用的功能类组件单元测试（Navigation Loading Navbar

- 常用页面的单元测试
  a new_feature_announcements page
  b user search page
  c group search
  d super user list page
  e country_accounts 各种tabs page

 