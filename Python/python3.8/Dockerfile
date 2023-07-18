# Ascend-infer开发环境
ARG Operation_VERSION

FROM  ${Operation_VERSION}
# image 标签
MAINTAINER jadehh@live.com
##安装字体
ARG Operation_VERSION

ENV LANG=C.UTF-8
RUN rm -r /etc/apt/sources.list
RUN if [ "$Operation_VERSION" = "ubuntu:20.04" ];\
    then \
    echo "deb http://mirrors.ustc.edu.cn/ubuntu/ focal main restricted universe multiverse" > /etc/apt/sources.list && \
    echo "deb-src http://mirrors.ustc.edu.cn/ubuntu/ focal main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb http://mirrors.ustc.edu.cn/ubuntu/ focal-security main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb-src http://mirrors.ustc.edu.cn/ubuntu/ focal-security main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb http://mirrors.ustc.edu.cn/ubuntu/ focal-updates main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb-src http://mirrors.ustc.edu.cn/ubuntu/ focal-updates main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb http://mirrors.ustc.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb-src http://mirrors.ustc.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse" >> /etc/apt/sources.list; \
    echo "deb http://mirrors.ustc.edu.cn/ubuntu/ focal-backports main restricted universe multiverse" >> /etc/apt/sources.list; \
    echo "deb-src http://mirrors.ustc.edu.cn/ubuntu/ focal-backports main restricted universe multiverse" >> /etc/apt/sources.list; \
    fi
## 安装 wget vim
RUN apt-get update && apt-get install -y python3-dev python3-pip  && rm -rf /var/lib/apt/lists/*
RUN ln -sT /usr/bin/python3 /usr/bin/python