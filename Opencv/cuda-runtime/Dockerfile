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

## 换源
RUN rm -r /etc/apt/sources.list
# 默认注释了源码仓库，如有需要可自行取消注释

RUN if [ "$Operation_VERSION" = "ubuntu18.04" ];\
    then \
    echo "deb https://mirrors.ustc.edu.cn/ubuntu/ bionic main restricted universe multiverse" > /etc/apt/sources.list && \
    echo "deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-security main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-security main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse" >> /etc/apt/sources.list; \
    fi

RUN if [ "$Operation_VERSION" = "ubuntu20.04" ];\
    then \
    echo "deb https://mirrors.ustc.edu.cn/ubuntu/ jammy main restricted universe multiverse" > /etc/apt/sources.list && \
    echo "# deb-src https://mirrors.ustc.edu.cn/ubuntu/ jammy main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb https://mirrors.ustc.edu.cn/ubuntu/ jammy-security main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "# deb-src https://mirrors.ustc.edu.cn/ubuntu/ jammy-security main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb https://mirrors.ustc.edu.cn/ubuntu/ jammy-updates main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "# deb-src https://mirrors.ustc.edu.cn/ubuntu/ jammy-updates main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb https://mirrors.ustc.edu.cn/ubuntu/ jammy-backports main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "# deb-src https://mirrors.ustc.edu.cn/ubuntu/ jammy-backports main restricted universe multiverse" >> /etc/apt/sources.list; \
    fi
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys A4B469963BF863CC
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
RUN wget https://gh.con.sh/https://github.com/jadehh/OpencvCapture/releases/download/v0.0.0.8/OpencvCapture-${Operation_VERSION} && chmod a+x OpencvCapture-${Operation_VERSION} && mv  OpencvCapture-${Operation_VERSION} OpencvCapture

