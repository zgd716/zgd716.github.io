---
layout: post
title:  "docker 使用gpu"
date: 2020-12-1 10:30:00
categories: nlp
tags: [nlp,docker,gpu,deployment]
---
<!-- 数学公式 -->
<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {
      skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
      inlineMath: [['$','$']]
    }
  });
</script>

docker中使用gpu<!-- more -->

### 在 Ubuntu/CentOS 上使用docker安装nvidia-docker2

安装nvidia-docker2

curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -

distribution=$(. /etc/os-release;echo $ID$VERSION_ID)

curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list

sudo apt-get update

sudo apt-get install nvidia-docker2

sudo pkill -SIGHUP dockerd

修改/etc/docker/daemon.json

{
    "default-runtime": "nvidia",
    "runtimes": {
        "nvidia": {
            "path": "/usr/bin/nvidia-container-runtime",
            "runtimeArgs": [],
            "registry-mirrors": ["https://gemfield.mirror.aliyuncs.com"]
        }
    }
}


sudo systemctl restart docker



sudo  docker run --runtime nvidia nvidia/cuda:9.0-base nvidia-smi

 

注意：Docker 19.03以上版本请使用NVIDIA Container Toolkit 工具包




