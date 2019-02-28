---
layout: post
title:  "tensorflow模型+flask+nginx+uwsgi+docker部署"
date: 2019-01-20 10:30:00
categories: deployment
tags: [docker,tensorflow,flask,nginx,uwsgi,docker]
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

tensorflow模型训练完以后，如何进行部署？很容易想到可以通过rest api提供接口的方式，使用flask+nginx+uwsgi很容易实现,为了部署方便，本文使用docker部署训练好的tensorflow模型。<!-- more -->)

##  1、简介

tensorflow model训练完后如何部署：1、使用tensorflow serving模式；2、使用flask  访问模型提供rest api方式

##  2、部署

<a href='https://github.com/zgd716/fasttext_docker'>代码</a>

-data    存放数据

-vocabs  存放字典文件

-runs    存放模型及tensorboard文件

-data_helper.py   处理数据

-config.py        配置文件

-fast_text.py     FastText类

-train.py         训练模型

-predict.py       预测

注意：train.py在训练模型的时候会生成vocabs文件夹，用来存储字典词字典、标签相关对象

项目中的main.py是flask项目的入口

为了使用docker部署，Dockerfile中使用joelogan/keras-tensorflow-flask-uwsgi-nginx-docker基础镜像

直接使用docker  build -t fasttext-image .  生成镜像

docker run -d --name fasttext-container -p 8989:80 fasttext-image  生成容器

<img src='/imgs/employment/tfmodel_flask_docker.jpg'>

