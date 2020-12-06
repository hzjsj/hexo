---
title: 使用 Docker 部署WordPress博客
tags:
    - 博客
    - Docker
cover_picture: https://687a-hzpc-1258873690.tcb.qcloud.la/cloudbase-cms/upload/2020-12-04/y0wJQYuxfBT0XzIi-2020120421513404.png
---
## Docker 介绍

Docker 是一个开源的应用容器引擎，基于 Go 语言 并遵从 Apache2.0 协议开源。
Docker 可以让开发者打包他们的应用以及依赖包到一个轻量级、可移植的容器中，然后发布到任何流行的 Linux 机器上，也可以实现虚拟化。

## Docker 安装

**Docker 官网**：[https://www.docker.com/get-started](https://www.docker.com/get-started)

现在 Docker 有专门的 Win10 专业版系统的安装包，需要开启 Hyper-V。
![20201204212243.png](https://687a-hzpc-1258873690.tcb.qcloud.la/cloudbase-cms/upload/2020-12-04/MbALS-DswNN2Wroa-20201204212243.png)

**阿里云镜像加速**
阿里云镜像获取地址：[https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors](https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors)，登陆后，左侧菜单选中镜像加速器就可以看到你的专属地址了：
![2020120421321802.png](https://687a-hzpc-1258873690.tcb.qcloud.la/cloudbase-cms/upload/2020-12-04/MFDaUYlENiMVjWq_-2020120421321802.png)

**在设置—Docker Engine 选项中填写加速地址**
![2020120421352403.png](https://687a-hzpc-1258873690.tcb.qcloud.la/cloudbase-cms/upload/2020-12-04/DBpe-9oZTe99FOPX-2020120421352403.png)

## Docker 安装 MySQL

查看可用的 MySQL 版本

```powershell
docker search mysql
```

拉取最新的 MySQL 镜像

```powershell
docker pull mysql:latest
```

查看本地镜像

```powershell
docker images
```

运行容器

```powershell
docker run -p 3306:3306 --name mysql -e MYSQL_ROOT_PASSWORD=123456 -d mysql
```

参数说明：

- **-p 3306:3306 ：** 映射容器服务的 3306 端口到宿主机的 3306 端口，外部主机可以直接通过 宿主机 `ip:3306` 访问到 MySQL 的服务
- **MYSQL_ROOT_PASSWORD=123456：** 设置 MySQL 服务 root 用户的密码

## Docker 安装 WordPress

输入一下命令，表示使用mysql来启动WordPress

```powershell
docker run --name wordpress --link mysql:mysql -p 80:80 -d wordpress
```

此时，WordPress项目就跑起来了
在本机输入localhost ，效果如下
![2020120421513404.png](https://687a-hzpc-1258873690.tcb.qcloud.la/cloudbase-cms/upload/2020-12-04/y0wJQYuxfBT0XzIi-2020120421513404.png)
![2020120421563705.png](https://687a-hzpc-1258873690.tcb.qcloud.la/cloudbase-cms/upload/2020-12-04/sJupynIa-ns_Uzz9-2020120421563705.png)

## 关机后再次启动

**需要先把 mysql 启动起来，然后再启动WordPress**

查看 CONTAINER ID

```powershell
docker ps
```

启动

```powershell
docker start 82220b303931
```

**或者直接在 Containers / Apps 选项中点击启动**
![2020120421563706.png](https://687a-hzpc-1258873690.tcb.qcloud.la/cloudbase-cms/upload/2020-12-04/-By-GibF-QyJcG0o-2020120421563706.png)
