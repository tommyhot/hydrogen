---
layout: post
title: git基础使用
tags: git
stickie: true
---

程序员必备的git的基础用法，如创建分支，拉取代码，合并代码，推送代码，解决冲突，创建tag，推送tag，删除tag，拉取tag等.


### 查看分支列表
`git branch -a`
选项：-a：all的缩写，同时列出本地分支和远程分支。若不加该选项，则只列出本地分支。

### 修改分支名称
git branch -m 旧分支名 新分支名

### 删除本地分支
git branch -d 本地分支名或git branch -D 本地分支名
选项：

-d：delete的缩写，会在删除前检查merge状态（其与上游分支或者与head）。
-D：是--delete --force的简写，它会直接删除。
### 删除远程分支
git push origin --delete 远程分支名

### 推送远程分支
git push origin 远程分支名或git push -f origin 远程分支名
选项：

-f：是--force的简写，表示强制覆盖远程分支。
### 打标签
git tag 标签名或git tag -a 标签名 -m "注释"

### 推送标签
git push origin 标签名

### 删除本地标签
git tag -d 标签名

### 删除远程标签
git push origin :refs/tags/标签名

### 同步远程标签到本地
#### 删除本地所有标签
git tag -l | xargs git tag -d

#### 拉取远程所有标签
git fetch --tags

### 查看远程仓库与本地仓库的关系
git remote show origin

### 清理本地无效的远程追踪分支
git remote prune origin

#### 删除本地指定的远程仓库地址
git remote remove 远程仓库地址（如：origin）

### 添加本地指定的远程仓库地址
git remote add origin 远程仓库地址（如：git@192.168.3.251:jaron/test.git）

### 拉取远程分支并创建本地分支
git checkout -b 本地分支名 origin/远程分支名

### 统计当前分支提交次数
git log --oneline | wc -l
windows平台下没有wc指令，需要使用：git log --oneline | find /v /c ""

### 在仓库中首次拉取子模块
git submodule update --init --recursive

### 在仓库中更新子模块
git submodule update --recursive --remote

### 设置CRLF和LF
* 提交时转换为LF，检出时转换为CRLF
git config --global core.autocrlf true
* 提交时转换为LF，检出时不转换
git config --global core.autocrlf input
* 提交检出均不转换
git config --global core.autocrlf false
* 拒绝提交包含混合换行符的文件
git config --global core.safecrlf true
* 允许提交包含混合换行符的文件
git config --global core.safecrlf false
* 提交包含混合换行符的文件时给出警告
git config --global core.safecrlf warn
