---
layout: post
title: Python开发环境
tags: python
stickie: true
---


这里记录的是Python下载、安装、环境配置等入门操作，包含pip包管理工具的使用，虚拟环境的创建，构建等等功能，快速搭建python环境。
更新：2023-07-05


### 安装python

* 从镜像地址下载 [https://registry.npmmirror.com/binary.html?path=python/](https://registry.npmmirror.com/binary.html?path=python/)

* 源码编译

```shell
sudo yum install -y sqlite sqlite-devel
tar -xf Python-3.12.4.tar.xz
./configure --enable-optimizations --prefix=/runtime/python3.12
make install
```

### pip 相关

* 设置pypi镜像地址

```shell
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```

### 虚拟环境相关

* pipenv
1. 安装 `pip install pipenv`
2. 使用 `pipenv shell`
3. 指定python版本 `pipenv shell --python=path`

* poerty
1. config文件目录：`\Users\huangm\AppData\Roaming\pypoetry`	环境变量：`POETRY_CACHE_DIR` 也可以控制 `cache-dir` 
2. poetry config http-basic.local username password
3. poetry config repositories.local http://pypi
4. `poetry install`报找不到包错误时使用`poetry cache clear <repo> --all`

### 自定site-packages位置：
在系统site-packages目录下新建 mysite.pth
```python
import site;site.addsitedir('<your-custom-sitedir>')
```
或者在 pythonpath 新建 sitecustomize.py

### 从git安装python包
通过git安装时，如果配置的是无法访问的地址，可以需要加 `.gitconfig` 文件里面写好 `insteadOf`
```
[url "http://x.x.x.x/xxx"]
    insteadOf = ssh://git@donghua.men/~/y/
	
eriskit = {git = "ssh://git@donghua.men/~/y/pyeriskit.git"}
```

### 发布包到私有pypi

​	使用 pypiserver

​	http://pypi

​	配置.pypirc文件，可以放用户名和密码 
​	```
​		[distutils]
​			index-servers =
​				local


		[local]
			repository: http://pypi
			username: xxx
			password: xxx
	```
	两种上传方法
	```shell
	python setup.py bdist_wheel upload -r local
    python setup.py sdist upload -r local
    twine upload -r local dist/*.whl # pip install twine
    ```


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