---
layout: post
title: anaconda-python虚拟环境
tags: python
stickie: true
---


```sh
conda create -n python37 python=3.7
source activate python37
pip install ipykernel
python -m ipykernel install python37
```