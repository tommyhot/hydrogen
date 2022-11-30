---
layout: post
title: anaconda-python虚拟环境
tags: python
---


```sh
conda create -n python37 python=3.7
source activate python37
pip install ipykernel
python -m ipykernel install python37
```

### pypi国内源
* 阿里源
```
[global]
index-url = http://mirrors.aliyun.com/pypi/simple/ 

[install]
trusted-host = mirrors.aliyun.com
```

	