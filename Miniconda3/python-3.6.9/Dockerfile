# Miniconda3Dockerfile
FROM  jadehh/miniconda3:amd64-4.9.2
# image 标签
MAINTAINER jadehh@live.com

RUN conda create -n python3.6.9 python=3.6.9 -y
RUN echo "source activate python3.6.9" >> /root/.bashrc


## pip换源
RUN rm -r /root/.pip
RUN mkdir /root/.pip/
RUN touch /root/.pip/pip.conf
RUN echo "[global]" >> /root/.pip/pip.conf
RUN echo "index-url = https://mirrors.bfsu.edu.cn/pypi/web/simple" >> /root/.pip/pip.conf
RUN echo "trusted-host = mirrors.bfsu.edu.cn" >> /root/.pip/pip.conf

