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


## 安装Conda
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
RUN conda create -n  paddletorch python=3.6 -y

## 下载expat
RUN wget https://mirrors.bfsu.edu.cn/anaconda/pkgs/main/linux-64/expat-2.4.9-h6a678d5_0.tar.bz2
RUN tar  -xvf expat-2.4.9-h6a678d5_0.tar.bz2
RUN cp -r lib/libexpat.* /usr/local/opencv-4.5.2/

## 安装numpy
RUN wget https://pypi.tuna.tsinghua.edu.cn/packages/14/32/d3fa649ad7ec0b82737b92fefd3c4dd376b0bb23730715124569f38f3a08/numpy-1.19.5-cp36-cp36m-manylinux2010_x86_64.whl
RUN unzip numpy-1.19.5-cp36-cp36m-manylinux2010_x86_64.whl
RUN mv numpy/ /usr/local/site-packages/ &&  cp -r numpy.libs/ /usr/local/site-packages/

## 安装Paddle
RUN wget  https://pypi.tuna.tsinghua.edu.cn/packages/f3/50/229d55dae20da61902e9979d68a30fc959ca9c6673b6c59d2396def08187/paddlepaddle_gpu-2.3.2-cp36-cp36m-manylinux1_x86_64.whl#sha256=277c8001374b060e06a5ca5493bc673c2d3ab8f5c083cbbaf7d7eb56b2d455b6
RUN unzip  paddlepaddle_gpu-2.3.2-cp36-cp36m-manylinux1_x86_64.whl
RUN cp -r paddle /usr/local/site-packages/

## 安装decorator
RUN wget https://pypi.tuna.tsinghua.edu.cn/packages/d5/50/83c593b07763e1161326b3b8c6686f0f4b0f24d5526546bee538c89837d6/decorator-5.1.1-py3-none-any.whl
RUN unzip  decorator-5.1.1-py3-none-any.whl
RUN cp -r decorator.py  /usr/local/site-packages/
## 安装six
RUN  wget https://pypi.tuna.tsinghua.edu.cn/packages/d9/5a/e7c31adbe875f2abbb91bd84cf2dc52d792b5a01506781dbcf25c91daf11/six-1.16.0-py2.py3-none-any.whl
RUN unzip  six-1.16.0-py2.py3-none-any.whl
RUN cp -r six.py  /usr/local/site-packages/

## 安装protobuf
RUN wget https://pypi.tuna.tsinghua.edu.cn/packages/8f/8e/06fc0df62dd80a32739b51bb3256f1417349eb5c3899f6ccab3796937458/protobuf-3.19.6-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl
RUN unzip protobuf-3.19.6-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl
RUN  cp -r google/ /usr/local/site-packages/




## 安装requests
RUN wget https://pypi.tuna.tsinghua.edu.cn/packages/2d/61/08076519c80041bc0ffa1a8af0cbd3bf3e2b62af10435d269a9d0f40564d/requests-2.27.1-py2.py3-none-any.whl
RUN unzip requests-2.27.1-py2.py3-none-any.whl
RUN  cp -r requests/ /usr/local/site-packages/

RUN wget https://pypi.tuna.tsinghua.edu.cn/packages/7b/f5/890a0baca17a61c1f92f72b81d3c31523c99bec609e60c292ea55b387ae8/urllib3-1.26.15-py2.py3-none-any.whl
RUN unzip urllib3-1.26.15-py2.py3-none-any.whl
RUN  cp -r urllib3/ /usr/local/site-packages/

RUN wget  https://pypi.tuna.tsinghua.edu.cn/packages/ea/0f/2fa195c2d8c6fe0b3dc2df5fc6ac6b8dbd005ea30aaa0fa43eca88b8c664/Pillow-8.4.0-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl
RUN unzip Pillow-8.4.0-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl
RUN cp -r PIL /usr/local/site-packages/ && cp -r  Pillow.libs/ /usr/local/site-packages/


RUN wget https://pypi.tuna.tsinghua.edu.cn/packages/c3/88/97eef84f48fa04fbd6750e62dcceafba6c63c81b7ac1420856c8dcc0a3f9/astor-0.8.1-py2.py3-none-any.whl
RUN unzip astor-0.8.1-py2.py3-none-any.whl
RUN cp -r astor /usr/local/site-packages/


RUN wget https://pypi.tuna.tsinghua.edu.cn/packages/bc/19/404708a7e54ad2798907210462fd950c3442ea51acc8790f3da48d2bee8b/opt_einsum-3.3.0-py3-none-any.whl
RUN unzip opt_einsum-3.3.0-py3-none-any.whl
RUN cp -r opt_einsum /usr/local/site-packages/

RUN wget https://pypi.tuna.tsinghua.edu.cn/packages/06/b3/24afc8868eba069a7f03650ac750a778862dc34941a4bebeb58706715726/charset_normalizer-2.0.12-py3-none-any.whl
RUN unzip charset_normalizer-2.0.12-py3-none-any.whl
RUN cp -r charset_normalizer /usr/local/site-packages/



RUN wget  https://pypi.tuna.tsinghua.edu.cn/packages/fc/34/3030de6f1370931b9dbb4dad48f6ab1015ab1d32447850b9fc94e60097be/idna-3.4-py3-none-any.whl
RUN unzip idna-3.4-py3-none-any.whl
RUN cp -r idna /usr/local/site-packages/

RUN  wget  https://download.pytorch.org/whl/cu100/torch-1.2.0-cp36-cp36m-manylinux1_x86_64.whl


RUN unzip torch-1.2.0-cp36-cp36m-manylinux1_x86_64.whl
RUN cp -r torch /usr/local/site-packages/

