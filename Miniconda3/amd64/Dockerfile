# Miniconda3Dockerfile
FROM  jadehh/ubuntu:amd64-18.04
# image 标签
MAINTAINER jadehh@live.com

## 安装 wget vim
RUN apt-get update
RUN apt-get install -y wget vim  gcc

## pip换源
RUN mkdir /root/.pip/
RUN touch /root/.pip/pip.conf
RUN echo "[global]" >> /root/.pip/pip.conf
RUN echo "index-url = https://pypi.tuna.tsinghua.edu.cn/simple" >> /root/.pip/pip.conf
RUN echo "trusted-host = pypi.tuna.tsinghua.edu.cn" >> /root/.pip/pip.conf


## 安装MiniConda3
RUN wget https://mirrors.bfsu.edu.cn/anaconda/miniconda/Miniconda3-py37_4.9.2-Linux-x86_64.sh
RUN bash Miniconda3-py37_4.9.2-Linux-x86_64.sh -b -p /root/miniconda3/

## 设置Miniconda3环境变量
ENV PATH /root/miniconda3/bin/:$PATH
RUN conda init bash
RUN rm -r Miniconda3-py37_4.9.2-Linux-x86_64.sh

