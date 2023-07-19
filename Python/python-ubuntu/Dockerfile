# Ascend-infer开发环境

ARG Operation_VERSION

FROM  ${Operation_VERSION}

ARG PYTHON_VERSION
# image 标签
MAINTAINER jadehh@live.com
##安装字体
ARG Operation_VERSION

ENV LANG=C.UTF-8
RUN rm -r /etc/apt/sources.list

RUN echo "deb http://mirrors.ustc.edu.cn/ubuntu/ bionic main restricted universe multiverse" > /etc/apt/sources.list && \
    echo "deb-src http://mirrors.ustc.edu.cn/ubuntu/ bionic main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb http://mirrors.ustc.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb-src http://mirrors.ustc.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb http://mirrors.ustc.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb-src http://mirrors.ustc.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb http://mirrors.ustc.edu.cn/ubuntu/ bionic-security main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb-src http://mirrors.ustc.edu.cn/ubuntu/ bionic-security main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb http://mirrors.ustc.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb-src http://mirrors.ustc.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse" >> /etc/apt/sources.list
## 安装Python
RUN apt-get update && apt-get install -y wget  build-essential zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev libsqlite3-dev wget libbz2-dev && rm -rf /var/lib/apt/lists/*
RUN wget https://www.python.org/ftp/python/${PYTHON_VERSION}/Python-${PYTHON_VERSION}.tgz && tar -xf Python-${PYTHON_VERSION}.tgz && rm Python-${PYTHON_VERSION}.tgz && cd  Python-${PYTHON_VERSION}/ && ./configure --enable-shared && make -j $(nproc) &&  make altinstall && rm -r Python-${PYTHON_VERSION}/
RUN mv /usr/local/lib/libpython${PYTHON_VERSION%.*}.so.1.0 /usr/lib/x86_64-linux-gnu/
RUN ln -sT /usr/lib/x86_64-linux-gnu/libpython${PYTHON_VERSION%.*}.so.1.0 /usr/lib/x86_64-linux-gnu/libpython${PYTHON_VERSION%.*}.so
RUN ln -sT /usr/lib/x86_64-linux-gnu/libpython${PYTHON_VERSION%.*}.so.1.0 /usr/lib/x86_64-linux-gnu/libpython${PYTHON_VERSION%%.*}.so
RUN mkdir /root/.pip/
RUN touch /root/.pip/pip.conf
RUN echo "[global]" >> /root/.pip/pip.conf
RUN echo "index-url = http://mirrors.bfsu.edu.cn/pypi/web/simple" >> /root/.pip/pip.conf
RUN echo "trusted-host = mirrors.bfsu.edu.cn" >> /root/.pip/pip.conf
RUN  ln -sT /usr/local/bin/python${PYTHON_VERSION%.*} /usr/bin/python && ln -sT /usr/local/bin/pip${PYTHON_VERSION%.*} /usr/bin/pip && pip install  --upgrade pip



