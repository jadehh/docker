# Opencv开发环境
ARG CUDA_VERSION
ARG CUDNN_VERSION

FROM  nvidia/cuda:${CUDA_VERSION}-cudnn${CUDNN_VERSION}-runtime-ubuntu18.04
ARG CUDA_VERSION
ARG CUDNN_VERSION
ARG CUDA_ARCH_BIN
ARG PYTHON_VERSION
# image 标签
MAINTAINER jadehh@live.com
## 设置语言
ENV LANG=C.UTF-8
RUN echo "CUDA版本为:${CUDA_VERSION}"
RUN echo "CUDNN版本为:${CUDNN_VERSION}"


RUN if [ "$CUDA_VERSION" != "10.0" ];\
    then \
      ## 去除docker容器的输出 \
    rm /opt/nvidia/nvidia_entrypoint.sh && \
    echo '#!/bin/bash' > /opt/nvidia/nvidia_entrypoint.sh  && \
    echo 'if [[ $# -eq 0 ]]; then' >> /opt/nvidia/nvidia_entrypoint.sh && \
    echo 'exec "/bin/bash"'  >> /opt/nvidia/nvidia_entrypoint.sh && \
    echo 'else'  >> /opt/nvidia/nvidia_entrypoint.sh && \
    echo '  exec "$@"' >> /opt/nvidia/nvidia_entrypoint.sh && \
    echo 'fi' >> /opt/nvidia/nvidia_entrypoint.sh && \
    chmod a+x  /opt/nvidia/nvidia_entrypoint.sh ; \
    fi
## 换源
RUN rm -r /etc/apt/sources.list
# 默认注释了源码仓库，如有需要可自行取消注释
RUN echo "deb https://mirrors.ustc.edu.cn/ubuntu/ bionic main restricted universe multiverse" > /etc/apt/sources.list && \
    echo "deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-security main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-security main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse" >> /etc/apt/sources.list

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys A4B469963BF863CC
RUN apt-get update
RUN apt-get install -y wget unzip  && rm -rf /var/lib/apt/lists/*

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
RUN wget https://gh.con.sh/https://github.com/jadehh/opencv/releases/download/4.8.0/opencv-cuda-${CUDA_VERSION}-cudnn${CUDNN_VERSION}-arch-${CUDA_ARCH_BIN}-py${PYTHON_VERSION%.*}.gz   && tar -xvf  opencv-cuda-${CUDA_VERSION}-cudnn${CUDNN_VERSION}-arch-${CUDA_ARCH_BIN}-py${PYTHON_VERSION%.*}.gz   && rm opencv-cuda-${CUDA_VERSION}-cudnn${CUDNN_VERSION}-arch-${CUDA_ARCH_BIN}-py${PYTHON_VERSION%.*}.gz
RUN echo "/usr/local/opencv" > /etc/ld.so.conf.d/opencv.conf
RUN wget https://gh.con.sh/https://github.com/jadehh/OpencvCapture/releases/download/v0.0.1.5/OpencvCapture-py${PYTHON_VERSION%.*}  && mv  OpencvCapture-py${PYTHON_VERSION%.*} OpencvCapture && chmod a+x OpencvCapture

## 安装numpy
RUN mkdir /usr/local/site-packages
RUN wget http://mirrors.bfsu.edu.cn/pypi/web/packages/d0/55/559e6f455a066e12058330377259a106b7fefa41c15dbdb1b71070cec429/numpy-1.25.1-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl && mv numpy-1.25.1-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl numpy.zip && unzip numpy.zip && mv /numpy* /usr/local/site-packages/ && rm -r /usr/local/site-packages/numpy.zip
