# Opencv开发环境
ARG Operation_VERSION
ARG CUDA_VERSION
ARG CUDNN_VERSION

FROM  nvidia/cuda:${CUDA_VERSION}-cudnn${CUDNN_VERSION}-runtime-${Operation_VERSION}
ARG Operation_VERSION
ARG CUDA_VERSION
ARG CUDNN_VERSION
ARG CUDA_ARCH_BIN

# image 标签
MAINTAINER jadehh@live.com
## 设置语言
ENV LANG=C.UTF-8
RUN echo "操作系统为:${Operation_VERSION}"
RUN echo "CUDA版本为:${CUDA_VERSION}"
RUN echo "CUDNN版本为:${CUDNN_VERSION}"


### 换源
RUN rm -r /etc/apt/sources.list
# 默认注释了源码仓库，如有需要可自行取消注释
RUN echo "deb https://mirrors.ustc.edu.cn/ubuntu/ jammy main restricted universe multiverse" > /etc/apt/sources.list
RUN echo "# deb-src https://mirrors.ustc.edu.cn/ubuntu/ jammy main restricted universe multiverse" >> /etc/apt/sources.list

RUN echo "deb https://mirrors.ustc.edu.cn/ubuntu/ jammy-security main restricted universe multiverse" >> /etc/apt/sources.list
RUN echo "# deb-src https://mirrors.ustc.edu.cn/ubuntu/ jammy-security main restricted universe multiverse" >> /etc/apt/sources.list

RUN echo "deb https://mirrors.ustc.edu.cn/ubuntu/ jammy-updates main restricted universe multiverse" >> /etc/apt/sources.list
RUN echo "# deb-src https://mirrors.ustc.edu.cn/ubuntu/ jammy-updates main restricted universe multiverse" >> /etc/apt/sources.list

RUN echo "deb https://mirrors.ustc.edu.cn/ubuntu/ jammy-backports main restricted universe multiverse" >> /etc/apt/sources.list
RUN echo "# deb-src https://mirrors.ustc.edu.cn/ubuntu/ jammy-backports main restricted universe multiverse" >> /etc/apt/sources.list


RUN apt-get update
RUN apt-get install -y wget  && rm -rf /var/lib/apt/lists/*

## 安装字体
RUN wget -P /usr/share/fonts/ https://gh.con.sh/https://github.com/jadehh/pythonTools/releases/download/v1.3.9/simhei.ttf

## 解决时间问题
RUN mkdir /usr/share/zoneinfo/
RUN wget -P /usr/share/zoneinfo/ https://gh.con.sh/https://github.com/jadehh/pythonTools/releases/download/v1.3.9/PRC
RUN ln -sf /usr/share/zoneinfo/PRC /etc/localtime

## 新建日志文件
RUN mkdir /home/jade
RUN touch /home/jade/test.log

RUN echo "更新opencv"
RUN wget https://gh.con.sh/https://github.com/jadehh/opencv/releases/download/4.8.0/opencv-cuda-${CUDA_VERSION}-cudnn${CUDNN_VERSION}-arch-${CUDA_ARCH_BIN}-${Operation_VERSION}.tar.gz  && tar -xvf  opencv-cuda-${CUDA_VERSION}-cudnn${CUDNN_VERSION}-arch-${CUDA_ARCH_BIN}-${Operation_VERSION}.tar.gz  && rm opencv-cuda-${CUDA_VERSION}-cudnn${CUDNN_VERSION}-arch-${CUDA_ARCH_BIN}-${Operation_VERSION}.tar.gz
RUN echo "/usr/local/opencv" > /etc/ld.so.conf.d/opencv.conf
RUN wget https://gh.con.sh/https://github.com/jadehh/OpencvCapture/releases/download/v0.0.0.5/OpencvCapture && chmod a+x OpencvCapture




