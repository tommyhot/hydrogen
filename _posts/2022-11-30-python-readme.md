---
layout: post
title: Python开发环境
tags: python
stickie: true
---


这里记录的是Python下载、安装、环境配置等入门操作，包含pip包管理工具的使用，虚拟环境的创建，构建等等功能，快速搭建python环境。



### 安装python

* 从镜像地址下载 [https://registry.npmmirror.com/binary.html?path=python/](https://registry.npmmirror.com/binary.html?path=python/)


### pip 相关

* 设置pypi镜像地址

`pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple`

### 虚拟环境相关

* pipenv
1. 安装 `pip install pipenv`
2. 使用 `pipenv shell`
3. 指定python版本 `pipenv shell --python=3.8`

* poerty


### python 模块加密(Cython)
```python
import os.path
import shutil
from setuptools import Extension, Distribution
from Cython.Build import cythonize, build_ext

ext_modules = cythonize([Extension("xxx", ["xxx.py"])])
dist = Distribution({"ext_modules": ext_modules})
cmd = build_ext(dist)
cmd.ensure_finalized()
cmd.run()

for output in cmd.get_outputs():
	relative_extension = os.path.relpath(output, cmd.build_lib)
	shutil.copyfile(output, relative_extension)

```