---
layout: post
title: docker相关
tags: docker
---

Welcome to Hydrogen!<br>If you saw this post, your blog has been successfully deployed.So enjoy the fun of writing now!

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

# docker 删除<none>的镜像
unix：

docker rmi $(docker images --filter "dangling=true" -q --no-trunc)

windows:

for /f "tokens=*" %x in ('docker images -f "dangling=true" -q') do docker rmi  %x