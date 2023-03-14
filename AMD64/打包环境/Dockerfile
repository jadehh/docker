FROM  jadehh/ubuntu:amd64-18.04
# image 标签
MAINTAINER jadehh@live.com
RUN rm /etc/apt/sources.list
RUN echo deb https://mirrors.ustc.edu.cn/ubuntu/ bionic main restricted universe multiverse >> /etc/apt/sources.list
RUN echo deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic main restricted universe multiverse >> /etc/apt/sources.list
RUN echo deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse >> /etc/apt/sources.list
RUN echo deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse >> /etc/apt/sources.list

RUN echo deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse >> /etc/apt/sources.list
RUN echo deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse >> /etc/apt/sources.list
RUN echo deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-security main restricted universe multiverse >> /etc/apt/sources.list
RUN echo deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-security main restricted universe multiverse>> /etc/apt/sources.list
RUN echo deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse >> /etc/apt/sources.list
RUN echo deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse>> /etc/apt/sources.list

## pip换源
RUN mkdir /root/.pip/
RUN touch /root/.pip/pip.conf
RUN echo "[global]" >> /root/.pip/pip.conf
RUN echo "index-url = https://mirrors.bfsu.edu.cn/pypi/web/simple" >> /root/.pip/pip.conf
RUN echo "trusted-host = mirrors.bfsu.edu.cn" >> /root/.pip/pip.conf


RUN apt-get update
RUN apt-get install -y python3-dev
RUN apt-get install -y python3-pip
RUN ln -s /usr/bin/python3 /usr/bin/python
RUN ln -s /usr/bin/pip3 /usr/bin/pip
RUN pip install -U pip setuptools
## 清除缓存

RUN apt-get clean