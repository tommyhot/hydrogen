---
layout: post
title: docker相关
tags: docker
stickie: true
---

# docker 使用指南

### 从Dockerfile构建镜像
	docker build -t yhpds:1.0 .

### 查看正在运行的容器
	docker ps -a

### docker 删除容器
	docker rm f58743ac02e0

### docker 删除镜像
	docker rmi 2fb207faae13

### docker 运行
docker run it yhpds:1.1 运行entrypoint


docker logs -f  --tail=100 97f74a979d70 

