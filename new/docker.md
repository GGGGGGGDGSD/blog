## 安装
这个安装官网来没什么问题

2. 常用命令
 docker ps 查看本地当前运行的容器
 docker images  查看本机上的镜像
 docker run -it ubuntu /bin/bash 启动一个ubuntu shell
 docker run -dp 80:80 docker/getting-started 启动示范demo

## 镜像
- 查找镜像
  以从 Docker Hub 网站来搜索镜像，Docker Hub 网址为： https://hub.docker.com/
  也可以用docker search name 搜索

- 拉取镜像
  docker pull <name>

- remove 
   docker rmi <name>

- 创建镜像(重点)
   创建一个 Dockerfile 文件  通过 docker build 命令来构建一个镜像


## Docker Compose
  通过 Compose，您可以使用 YML 文件来配置应用程序需要的所有服务。然后，使用一个命令，就可以从 YML 文件配置中创建并启动所有服务

  - Compose 使用的三个步骤：
    使用 Dockerfile 定义应用程序的环境。

    使用 docker-compose.yml 定义构成应用程序的服务，这样它们可以在隔离环境中一起运行。

    最后，执行 docker-compose up 命令来启动并运行整个应用程序。