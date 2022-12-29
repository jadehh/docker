# Ascend-infer开发环境
FROM  ubuntu:18.04
# image 标签
MAINTAINER jadehh@live.com
##安装字体

ENV LANG=C.UTF-8
## 安装 wget vim
RUN apt-get update
RUN apt-get install -y wget vim  gcc

## 安装字体
RUN mkdir /usr/share/fonts
RUN wget -P /usr/share/fonts/ https://gh.con.sh/https://github.com/jadehh/pythonTools/releases/download/v1.3.9/simhei.ttf

## 解决时间问题
RUN mkdir /usr/share/zoneinfo/
RUN wget -P /usr/share/zoneinfo/ https://gh.con.sh/https://github.com/jadehh/pythonTools/releases/download/v1.3.9/PRC
RUN ln -sf /usr/share/zoneinfo/PRC /etc/localtime



## pip换源
RUN mkdir /root/.pip/
RUN touch /root/.pip/pip.conf
RUN echo "[global]" >> /root/.pip/pip.conf
RUN echo "index-url = https://pypi.tuna.tsinghua.edu.cn/simple" >> /root/.pip/pip.conf
RUN echo "trusted-host = pypi.tuna.tsinghua.edu.cn" >> /root/.pip/pip.conf


## 安装MiniConda3
RUN wget https://mirrors.bfsu.edu.cn/anaconda/miniconda/Miniconda3-py37_4.9.2-Linux-aarch64.sh
RUN bash Miniconda3-py37_4.9.2-Linux-aarch64.sh -b -p /root/miniconda3/

## 设置Miniconda3环境变量
ENV PATH /root/miniconda3/bin/:$PATH
RUN conda init bash
RUN rm -r Miniconda3-py37_4.9.2-Linux-aarch64.sh

## pip环境设置
RUN pip install https://gh.con.sh/https://github.com/jadehh/pythonTools/releases/download/OpencvToolsV1.1.6/opencv_tools-1.1.6-py3-none-any.whl && \
    pip install https://gh.con.sh/https://github.com/jadehh/pythonTools/releases/download/JadeV1.5.2/jade-1.5.2-py3-none-any.whl