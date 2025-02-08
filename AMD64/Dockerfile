# Ascend-infer开发环境
FROM  ubuntu:24.04
# image 标签
MAINTAINER jadehh@live.com

## 安装wget
RUN apt-get update  && apt-get install -y wget  && rm -rf /var/lib/apt/lists/*

## 安装字体
RUN mkdir /usr/share/fonts
RUN wget -P /usr/share/fonts/ https://github.com/jadehh/pythonTools/releases/download/v1.3.9/simhei.ttf

## 解决时间问题
RUN mkdir /usr/share/zoneinfo/
RUN wget -P /usr/share/zoneinfo/ https://github.com/jadehh/pythonTools/releases/download/v1.3.9/PRC
RUN ln -sf /usr/share/zoneinfo/PRC /etc/localtime

## 设置中文环境
ENV LANG=C.UTF-8

## 安装加密狗环境
RUN  wget http://192.168.40.215:8099/aksusbd_8.51-1_amd64.deb && dpkg -i aksusbd_8.51-1_amd64.deb && rm aksusbd_8.51-1_amd64.deb
RUN  wget http://192.168.40.215:8099/hasplm.ini && cp hasplm.ini /etc/hasplm/ && rm hasplm.ini

## 显示日志
RUN mkdir /home/jade
RUN touch /home/jade/test.log