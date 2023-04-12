<!--
 * @Author          : ZheZhang
 * @CreateDate      : 2023-03-27 09:08:58
 * @LastEditors     : ZhangBetter
 * @LastEditorsEmail: zhangzhenumberone@gmail.com
 * @LastEditTime    : 2023-04-12 17:31:41
 * @Description     : 著作权保护，转载请注明出处！
 * Copyright (c) 2023 by ZhangBetter Email: zhangzhenumberone@gmail.com, All Rights Reserved.
-->

# Docker 学习笔记
> **本片笔记主要记录 docker 学习过程**  

- [Docker 学习笔记](#docker-学习笔记)
- [在 WSL2 中安装 docker](#在-wsl2-中安装-docker)
  - [首先需要安装配置好 WSL2](#首先需要安装配置好-wsl2)
  - [安装步骤](#安装步骤)
- [常用命令](#常用命令)
  - [帮助启动类](#帮助启动类)

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