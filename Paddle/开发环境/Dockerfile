# Ascend-infer开发环境
FROM  nvidia/cuda:10.0-cudnn7-runtime-ubuntu18.04
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

## 安装wget
RUN apt-get update
RUN apt-get install -y wget libxcb* unzip

## 安装字体
RUN mkdir /usr/share/fonts
RUN wget -P /usr/share/fonts/ https://ghproxy.com/https://github.com/jadehh/pythonTools/releases/download/v1.3.9/simhei.ttf

## 解决时间问题
RUN mkdir /usr/share/zoneinfo/
RUN wget -P /usr/share/zoneinfo/ https://ghproxy.com/https://github.com/jadehh/pythonTools/releases/download/v1.3.9/PRC
RUN ln -sf /usr/share/zoneinfo/PRC /etc/localtime

## 设置中文环境
ENV LANG=C.UTF-8


# 软连接CUDA
RUN ln -s /usr/local/cuda/lib64/libcublas.so.10.0.130 /usr/local/cuda/lib64/libcublas.so
RUN ln -s /usr/local/cuda/lib64/libcudart.so.10.0.130 /usr/local/cuda/lib64/libcudart.so
RUN ln -s /usr/local/cuda/lib64/libcurand.so.10.0.130 /usr/local/cuda/lib64/libcurand.so
RUN ln -s /usr/local/cuda/lib64/libcusolver.so.10.0.130 /usr/local/cuda/lib64/libcusolver.so
RUN ln -s /usr/local/cuda/lib64/libcusparse.so.10.0.130 /usr/local/cuda/lib64/libcusparse.so
RUN ln -s /usr/local/cuda/lib64/libnppc.so.10.0.130 /usr/local/cuda/lib64/libnppc.so
RUN ln -s /usr/local/cuda/lib64/libnppial.so.10.0.130 /usr/local/cuda/lib64/libnppial.so
RUN ln -s /usr/local/cuda/lib64/libnppicc.so.10.0.130 /usr/local/cuda/lib64/libnppicc.so
RUN ln -s /usr/local/cuda/lib64/libnppicom.so.10.0.130 /usr/local/cuda/lib64/libnppicom.so
RUN ln -s /usr/local/cuda/lib64/libnppidei.so.10.0.130 /usr/local/cuda/lib64/libnppidei.so
RUN ln -s /usr/local/cuda/lib64/libnppif.so.10.0.130 /usr/local/cuda/lib64/libnppif.so
RUN ln -s /usr/local/cuda/lib64/libnppig.so.10.0.130 /usr/local/cuda/lib64/libnppig.so
RUN ln -s /usr/local/cuda/lib64/libnppim.so.10.0.130 /usr/local/cuda/lib64/libnppim.so
RUN ln -s /usr/local/cuda/lib64/libnppist.so.10.0.130 /usr/local/cuda/lib64/libnppist.so
RUN ln -s /usr/local/cuda/lib64/libnppisu.so.10.0.130 /usr/local/cuda/lib64/libnppisu.so
RUN ln -s /usr/local/cuda/lib64/libnppitc.so.10.0.130 /usr/local/cuda/lib64/libnppitc.so
RUN ln -s /usr/local/cuda/lib64/libnpps.so.10.0.130 /usr/local/cuda/lib64/libnpps.so
RUN ln -s /usr/local/cuda/lib64/libnvblas.so.10.0.130 /usr/local/cuda/lib64/libnvblas.so
RUN ln -s /usr/local/cuda/lib64/libnvgraph.so.10.0.130 /usr/local/cuda/lib64/libnvgraph.so
RUN ln -s /usr/local/cuda/lib64/libnvjpeg.so.10.0.130 /usr/local/cuda/lib64/libnvjpeg.so
RUN ln -s /usr/local/cuda/lib64/libnvrtc.so.10.0.130 /usr/local/cuda/lib64/libnvrtc.so
## cudnn安装
RUN wget https://ghproxy.com/https://github.com/jadehh/jadehh_file/releases/download/Container_NpuV1.0.1/cudnn-7.6.4.tar && \
    tar -xvf cudnn-7.6.4.tar && \
    mv cudnn/libcudnn.so.7.6.4 /usr/local/cuda/lib64 && \
    ln -s /usr/local/cuda/lib64/libcudnn.so.7.6.4 /usr/local/cuda/lib64/libcudnn.so && \
    rm cudnn-7.6.4.tar && rm -r cudnn

## pip换源
RUN mkdir /root/.pip/
RUN touch /root/.pip/pip.conf
RUN echo "[global]" >> /root/.pip/pip.conf
RUN echo "index-url = https://mirrors.bfsu.edu.cn/pypi/web/simple" >> /root/.pip/pip.conf
RUN echo "trusted-host = mirrors.bfsu.edu.cn" >> /root/.pip/pip.conf


RUN apt-get update && \
    apt-get install -y python3-dev && \
    apt-get install -y python3-pip && \
    ln -s /usr/bin/python3 /usr/bin/python && \
    ln -s /usr/bin/pip3 /usr/bin/pip && \
    pip install -U pip setuptools

## 安装opencv-python
RUN wget https://mirrors.bfsu.edu.cn/pypi/web/packages/35/7b/628da8b9f91342432a9432d900d5e2771c387969430e7d4a513dc6dd7804/opencv_python_headless-4.4.0.40-cp36-cp36m-manylinux2014_x86_64.whl --no-check-certificate && \
    unzip opencv_python_headless-4.4.0.40-cp36-cp36m-manylinux2014_x86_64.whl  && rm opencv_python_headless-4.4.0.40-cp36-cp36m-manylinux2014_x86_64.whl && \
    mv cv2/ /usr/local/site-packages/ && \
    rm -r opencv_python_headless-4.4.0.40.dist-info && \
    mv opencv_python_headless.libs/* /usr/lib/x86_64-linux-gnu/ && rm -r opencv_python_headless.libs

RUN wget https://paddle-wheel.bj.bcebos.com/2.1.3/linux/linux-gpu-cuda10.1-cudnn7-mkl-gcc5.4-avx/paddlepaddle_gpu-2.1.3.post101-cp36-cp36m-linux_x86_64.whl && \
    unzip paddlepaddle_gpu-2.1.3.post101-cp36-cp36m-linux_x86_64.whl && rm paddlepaddle_gpu-2.1.3.post101-cp36-cp36m-linux_x86_64.whl &&  \
    mv paddle /usr/local/site-packages/ && rm -r paddle* && rm _foo.cpython-36m-x86_64-linux-gnu.so && rm NGC-DL-CONTAINER-LICENSE

RUN wget https://gh.ddlc.top/https://github.com/jadehh/paddle/releases/download/v2.1.0-gpu-linux-py3.6/image.py && \
    mv image.py /usr/local/site-packages/paddle/dataset/

## 安装decorator
RUN wget https://pypi.tuna.tsinghua.edu.cn/packages/d5/50/83c593b07763e1161326b3b8c6686f0f4b0f24d5526546bee538c89837d6/decorator-5.1.1-py3-none-any.whl && \
    unzip  decorator-5.1.1-py3-none-any.whl && \
    mv decorator.py  /usr/local/site-packages/ && \
    rm -r decorator*

RUN pip install numpy

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

RUN wget https://pypi.tuna.tsinghua.edu.cn/packages/06/b3/24afc8868eba069a7f03650ac750a778862dc34941a4bebeb58706715726/charset_normalizer-2.0.12-py3-none-any.whl &&  \
    unzip charset_normalizer-2.0.12-py3-none-any.whl  &&  \
    mv charset_normalizer /usr/local/site-packages/ &&  \
    rm -r charset_normalizer*

RUN wget https://mirrors.bfsu.edu.cn/pypi/web/packages/9d/19/59961b522e6757f0c9097e4493fa906031b95b3ebe9360b2c3083561a6b4/certifi-2023.5.7-py3-none-any.whl  && \
    unzip certifi-2023.5.7-py3-none-any.whl && \
    mv certifi /usr/local/site-packages/ &&  \
    rm -r certifi*



RUN wget https://mirrors.bfsu.edu.cn/pypi/web/packages/fa/39/5aae571e5a5f4de9c3445dae08a530498e5c53b0e74410eeeb0991c79047/gast-0.5.4-py3-none-any.whl  && \
    unzip gast-0.5.4-py3-none-any.whl && \
    mv gast /usr/local/site-packages/ &&  \
    rm -r gast*

RUN wget https://pypi.tuna.tsinghua.edu.cn/packages/c3/88/97eef84f48fa04fbd6750e62dcceafba6c63c81b7ac1420856c8dcc0a3f9/astor-0.8.1-py2.py3-none-any.whl &&  \
    unzip astor-0.8.1-py2.py3-none-any.whl &&  \
    mv astor /usr/local/site-packages/ &&  \
    rm -r astor*


RUN mkdir /home/jade
RUN touch /home/jade/test.log


