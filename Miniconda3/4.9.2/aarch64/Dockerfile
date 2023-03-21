# Miniconda3Dockerfile
FROM  jadehh/ubuntu:aarch-18.04
# image 标签
MAINTAINER jadehh@live.com

## 安装 wget vim
RUN apt-get update
RUN apt-get install -y wget vim  gcc

## 安装MiniConda3
RUN wget https://mirrors.bfsu.edu.cn/anaconda/miniconda/Miniconda3-py37_4.9.2-Linux-aarch64.sh
RUN bash Miniconda3-py37_4.9.2-Linux-aarch64.sh -b -p /root/miniconda3/

## 设置Miniconda3环境变量
ENV PATH /root/miniconda3/bin/:$PATH
RUN conda init bash
RUN rm -r Miniconda3-py37_4.9.2-Linux-aarch64.sh

