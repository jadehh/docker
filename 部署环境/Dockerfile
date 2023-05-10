# Ascend-infer开发环境
FROM  jadehh/opencv-4.5.2-cuda:10.0.3-cudnn7-runtime-ubuntu18.04
# image 标签
MAINTAINER jadehh@live.com
## 换源
RUN rm -r  /etc/apt/sources.list
RUN rm -r  /etc/apt/sources.list.d/*
RUN echo "deb  http://mirrors.aliyun.com/ubuntu/ xenial main" > /etc/apt/sources.list

## 安装wget
RUN apt-get update
RUN apt-get install -y wget unzip

## 安装字体
RUN mkdir /usr/share/fonts
RUN wget -P /usr/share/fonts/ https://ghproxy.com/https://github.com/jadehh/pythonTools/releases/download/v1.3.9/simhei.ttf

## 移动Opencv文件夹

RUN mkdir /usr/local/site-packages/
RUN mv /usr/local/opencv-4.5.2/cv2.cpython-36m-x86_64-linux-gnu.so /usr/local/site-packages/

## 设置中文环境
ENV LANG=C.UTF-8

## 下载expat
RUN wget https://mirrors.bfsu.edu.cn/anaconda/pkgs/main/linux-64/expat-2.4.9-h6a678d5_0.tar.bz2  && \
    tar  -xvf expat-2.4.9-h6a678d5_0.tar.bz2 && \
    mv lib/libexpat.* /usr/local/opencv-4.5.2/ && \
    rm -r expat*


## 安装Paddle
RUN wget  https://pypi.tuna.tsinghua.edu.cn/packages/f3/50/229d55dae20da61902e9979d68a30fc959ca9c6673b6c59d2396def08187/paddlepaddle_gpu-2.3.2-cp36-cp36m-manylinux1_x86_64.whl#sha256=277c8001374b060e06a5ca5493bc673c2d3ab8f5c083cbbaf7d7eb56b2d455b6 && \
    unzip  paddlepaddle_gpu-2.3.2-cp36-cp36m-manylinux1_x86_64.whl && \
    mv paddle /usr/local/site-packages/ && \
    rm -r paddle*

RUN wget https://gh.ddlc.top/https://github.com/jadehh/paddle/releases/download/v2.1.0-gpu-linux-py3.6/image.py && \
    mv image.py /usr/local/site-packages/paddle/dataset/

## 安装decorator
RUN wget https://pypi.tuna.tsinghua.edu.cn/packages/d5/50/83c593b07763e1161326b3b8c6686f0f4b0f24d5526546bee538c89837d6/decorator-5.1.1-py3-none-any.whl && \
    unzip  decorator-5.1.1-py3-none-any.whl && \
    mv decorator.py  /usr/local/site-packages/ && \
    rm -r decorator*

## 安装six
RUN  wget https://pypi.tuna.tsinghua.edu.cn/packages/d9/5a/e7c31adbe875f2abbb91bd84cf2dc52d792b5a01506781dbcf25c91daf11/six-1.16.0-py2.py3-none-any.whl && \
     unzip  six-1.16.0-py2.py3-none-any.whl && \
     mv six.py  /usr/local/site-packages/ && \
     rm -r six*

## 安装protobuf
RUN wget https://pypi.tuna.tsinghua.edu.cn/packages/8f/8e/06fc0df62dd80a32739b51bb3256f1417349eb5c3899f6ccab3796937458/protobuf-3.19.6-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl && \
    unzip protobuf-3.19.6-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl && \
    mv google/ /usr/local/site-packages/ && \
    rm -r protobuf*

## 安装requests
RUN wget https://pypi.tuna.tsinghua.edu.cn/packages/2d/61/08076519c80041bc0ffa1a8af0cbd3bf3e2b62af10435d269a9d0f40564d/requests-2.27.1-py2.py3-none-any.whl && \
    unzip requests-2.27.1-py2.py3-none-any.whl && \
    mv requests/ /usr/local/site-packages/ && \
    rm -r requests*

RUN wget https://pypi.tuna.tsinghua.edu.cn/packages/7b/f5/890a0baca17a61c1f92f72b81d3c31523c99bec609e60c292ea55b387ae8/urllib3-1.26.15-py2.py3-none-any.whl &&  \
    unzip urllib3-1.26.15-py2.py3-none-any.whl && \
    mv urllib3/ /usr/local/site-packages/ && \
    rm -r urllib3*

RUN wget  https://pypi.tuna.tsinghua.edu.cn/packages/ea/0f/2fa195c2d8c6fe0b3dc2df5fc6ac6b8dbd005ea30aaa0fa43eca88b8c664/Pillow-8.4.0-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl &&  \
    unzip Pillow-8.4.0-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl &&  \
    mv PIL /usr/local/site-packages/ && cp -r  Pillow.libs/ /usr/local/site-packages/ &&  \
    rm -r Pillow*


RUN wget https://pypi.tuna.tsinghua.edu.cn/packages/c3/88/97eef84f48fa04fbd6750e62dcceafba6c63c81b7ac1420856c8dcc0a3f9/astor-0.8.1-py2.py3-none-any.whl &&  \
    unzip astor-0.8.1-py2.py3-none-any.whl &&  \
    mv astor /usr/local/site-packages/ &&  \
    rm -r astor*


RUN wget https://pypi.tuna.tsinghua.edu.cn/packages/bc/19/404708a7e54ad2798907210462fd950c3442ea51acc8790f3da48d2bee8b/opt_einsum-3.3.0-py3-none-any.whl &&  \
    unzip opt_einsum-3.3.0-py3-none-any.whl &&  \
    mv opt_einsum /usr/local/site-packages/ &&  \
    rm -r opt_einsum*

RUN wget https://pypi.tuna.tsinghua.edu.cn/packages/06/b3/24afc8868eba069a7f03650ac750a778862dc34941a4bebeb58706715726/charset_normalizer-2.0.12-py3-none-any.whl &&  \
    unzip charset_normalizer-2.0.12-py3-none-any.whl  &&  \
    mv charset_normalizer /usr/local/site-packages/ &&  \
    rm -r charset_normalizer*



RUN wget  https://pypi.tuna.tsinghua.edu.cn/packages/fc/34/3030de6f1370931b9dbb4dad48f6ab1015ab1d32447850b9fc94e60097be/idna-3.4-py3-none-any.whl &&  \
    unzip idna-3.4-py3-none-any.whl &&  \
    mv idna /usr/local/site-packages/ &&  \
    rm -r idna*

RUN  wget https://gh.ddlc.top/https://github.com/jadehh/docker/releases/download/VideoStitchingV1.0.1/torch-1.2.0-cp36-cp36m-manylinux1_x86_64.whl &&  \
     unzip torch-1.2.0-cp36-cp36m-manylinux1_x86_64.whl &&  \
     mv torch /usr/local/site-packages/ &&  \
     rm -r torch* && rm -r caffe*

## 新建日志文件
RUN mkdir /home/jade
RUN touch /home/jade/test.log
