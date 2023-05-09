<!--
 * @Author          : ZheZhang
 * @CreateDate      : 2023-03-27 09:08:58
 * @LastEditors     : ZhangBetter
 * @LastEditorsEmail: zhangzhenumberone@gmail.com
 * @LastEditTime    : 2023-04-14 21:46:32
 * @Description     : 著作权保护，转载请注明出处！
 * Copyright (c) 2023 by ZhangBetter Email: zhangzhenumberone@gmail.com, All Rights Reserved.
-->

# Docker 学习笔记
> **本片笔记主要记录 docker 学习过程**  

* [Docker 学习笔记](#docker-学习笔记)
* [在 WSL2 中安装 docker](#在-wsl2-中安装-docker)
  * [首先需要安装配置好 WSL2](#首先需要安装配置好-wsl2)
  * [安装步骤](#安装步骤)
* [常用命令](#常用命令)
  * [帮助启动类](#帮助启动类)
  * [镜像命令](#镜像命令)
  * [容器命令](#容器命令)

***

# 在 WSL2 中安装 docker  
## 首先需要安装配置好 WSL2
> 参考[ WSL 配置](./WSL配置)  

## 安装步骤
* 确认系统版本为 CentOS 7 及以上  
`cat /etc/redhat-release`
* 卸载旧版本
  ```
  yum remove docker docker-client \
                    docker-client-latest \
                    docker-common \
                    docker-latest \
                    docker-latest-logrotate \
                    docker-logrotate \
                    docker-engine
  ```
* yum 安装 gcc 相关
  ```
  yum install -y gcc
  yum install -y gcc-c++
  ```
* 安装需要的软件包  
`yum install -y yum-utils`
* 设置stable镜像仓库  
`yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo`
* 更新 yum 索引  
`yum makecache`
* 安装 docker ce  
`yum -y install docker-ce docker-ce-cli containerd.io`
* 修改 `/usr/lib/systemd/system/docker.service` 文件
  ```
  #ExecStart=/usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock
  #ExecStart=/usr/bin/dockerd -H unix:// --containerd=/run/containerd/containerd.sock
  ExecStart=/usr/bin/dockerd
  ```
* 启动 docker  
`systemctl start docker`
* 检查 docker 状态  
  ```
  systemctl status docker
  docker version
  ```
* 运行 Hello-World  
`docker run hello-world`
# 常用命令
## 帮助启动类
* 启动，停止，重启，状态  
  ```
  systemctl start docker
  systemctl stop docker
  systemctl restart docker
  systemctl status docker
  ```
* 开机自启  
`systemctl enable docker`
* 查看 docker 概要信息  
`docker info`
* 查看 docker 命令帮助  
  ```
  docker --help
  docker [具体命令] --help
  ```
## 镜像命令
* 列出本地主机所有镜像  
  ```
  docker images [options]
  
  options:
  -a:列出包含历史镜像在内的所有镜像
  -q:只显示镜像id
  ```
* 搜索镜像
  ```
  docker search [options] [image_name]
  
  options:
  --limit:限制列出镜像的数量，默认25个
  ```
* 下载镜像  
  ```
  docker pull [image_name][:tag]
  
  举例：
  docker pull ubuntu 等价于 docker pull ubuntu:latest
  ```
* 查看镜像/容器/数据卷所占空间  
`docker system df`
* 删除镜像  
  ```
  docker rmi [image_id]
  docekr rmi -f [image_id] #删除单个镜像
  docker rmi -f image_name_0:tag image_name_1:tag #删除多个镜像
  docker rmi -f $(docker images -qa) #删除所有镜像
  ```
## 容器命令
* 新建/启动容器
  ```
  docker run [options] images [command] [argument]
  
  options:
  --name="容器新名字"：为容器指定一个新名称
  -d:后台运行容器并返回容器id，即启动守护式容器（后台运行）
  -i:以交互式模式运行容器，通常与 -t 一起使用
  -t:为容器重新分配一个伪终端，通常与 -i 一起使用
  -P:随机端口映射
  -p:指定端口映射
  
  举例：
  docker run -it image_name /bin/bash
  ```
* 列出当前正在运行的所有容器
  ```
  docker ps [options]
  
  options:
  -a:包含历史运行过的容器
  -l:显示最近创建的容器
  -n:显示最近创建的n个容器
  -q:静默模式。只显示容器编号
  ```
* 退出容器
  ```
  exit:退出后容器停止运行
  ctrl+p+q:退出后容器不停止运行
  ```
* 启动/停止/重启/强制停止容器
  ```
  docker start 容器id/容器name
  docker stop 容器id/容器name
  docker restart 容器id/容器name
  docker kill 容器id/容器name
  ```
* 删除已停止的容器
  ```
  docker rm 容器id
  
  #一次性删除多个容器实例：
  docker rm -f $(docker ps -a -q)
  docekr ps -a -q | xargs docker rm
  ```
* 启动守护式容器
  > 大部分情况下，希望docker的服务在后台运行，可以通过-d使服务在后台运行  

  ```
  docker run -d 容器名
  
  举例：
  docker run -d redis:6.0.8
  ```
* 查看容器日志  
`docker logs 容器id`
* 查看容器内运行的进程  
`docker top 容器id`
* 查看容器内部细节  
`docker inspect 容器id`
* 进入正在运行的容器并以命令行进行交互  
  ```
  docker exec -it 容器id /bin/bash
  docker attach 容器id
  
  区别：
  attach 直接进入容器启动命令的终端，不会启动新的进程，用exit退出，会导致容器的停止。
  exec 是在容器中打开新的终端，并且可以启动新的进程，用exit退出，不会导致容器的停止。
  
  举例：
  # 进入redis服务：
  docker exec -it 容器id /bin/bash
  docker exec -it 容器id redis-cli
  ```
* 从容器内拷贝主机文件到主机上  
`docker cp 容器id:容器内文件路径 主机路径`
* 导出/导入容器  
  ```
  # 导出：
  docker export 容器id > 文件名.tar
  # 导入：
  cat 文件名.tar | docker import - 镜像用户/镜像名:版本号
  ```