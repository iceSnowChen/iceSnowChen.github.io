---
title: docker安装zookeeper步骤
date: 2019-08-11 22:05:05
tags:
---

- 启动zookeeper:

  docker run -p 2181:2181 --name zookeeper --restart always -d zookeeper

- 通过客户端连接已运行的zookeeper:

  docker run -it --rm --link zookeeper:zookeeper zookeeper zkCli.sh -server zookeeper

- 进入zookeeper容器

  docker exec -it zookeeper bash

- Docker容器中的另一个应用程序连接到Zookeeper:

  docker run --name someApp --link zookeeper:zookeeper -d application-that-uses-zookeeper

