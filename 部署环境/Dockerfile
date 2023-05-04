# Ascend-infer开发环境
FROM  jadehh/opencv-4.5.2-cuda:10.0.3-cudnn7-runtime-ubuntu18.04
# image 标签
MAINTAINER jadehh@live.com
## 换源
RUN rm -r  /etc/apt/sources.list
RUN rm -r  /etc/apt/sources.list.d/*
RUN echo "deb  http://mirrors.aliyun.com/ubuntu/ xenial main" > /etc/apt/sources.list

## 安装wget
RUN apt-get update
RUN apt-get install -y wget unzip

## 安装字体
RUN mkdir /usr/share/fonts
RUN wget -P /usr/share/fonts/ https://ghproxy.com/https://github.com/jadehh/pythonTools/releases/download/v1.3.9/simhei.ttf

## 移动Opencv文件夹

RUN mkdir /usr/local/site-packages/
RUN mv /usr/local/opencv-4.5.2/cv2.cpython-36m-x86_64-linux-gnu.so /usr/local/site-packages/

## 设置中文环境
ENV LANG=C.UTF-8


## 安装Paddle环境









RUN mkdir /home/jade
RUN touch /home/jade/test.log
RUN apt-get purge -y wget unzip
RUN apt-get clean
