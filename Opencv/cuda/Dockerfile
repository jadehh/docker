# Opencv开发环境
ARG Operation_VERSION
ARG CUDA_VERSION
ARG CUDNN_VERSION
ARG CPU_THERAD_COMPILE
ARG CUDA_ARCH_BIN
FROM  nvidia/cuda:${CUDA_VERSION}-cudnn${CUDNN_VERSION}-devel-${Operation_VERSION}
ARG Operation_VERSION
ARG CUDA_VERSION
ARG CUDNN_VERSION
ARG CPU_THERAD_COMPILE
ARG CUDA_ARCH_BIN
# image 标签
MAINTAINER jadehh@live.com
## 设置语言
ENV LANG=C.UTF-8
RUN echo "操作系统为:${Operation_VERSION}"
RUN echo "CUDA版本为:${CUDA_VERSION}"
RUN echo "CUDNN版本为:${CUDNN_VERSION}"
RUN echo "CPU线程数为:${CPU_THERAD_COMPILE}"
RUN echo "计算能力为:${CUDA_ARCH_BIN}"

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

RUN sed -i "s%{GPG_EXE}\")' --%{GPG_EXE}\")' --batch --%g" /usr/bin/apt-key
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys A4B469963BF863CC

RUN apt-get update
RUN apt-get install -y wget unzip  cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev  libswscale-dev libopenblas-dev  libgstreamer-plugins-base1.0-dev libgstreamer1.0-dev python3-dev python3-numpy libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev  software-properties-common   && rm -rf /var/lib/apt/lists/*

## 安装字体
RUN wget -P /usr/share/fonts/ https://gh.con.sh/https://github.com/jadehh/pythonTools/releases/download/v1.3.9/simhei.ttf

## 解决时间问题
RUN mkdir /usr/share/zoneinfo/
RUN wget -P /usr/share/zoneinfo/ https://gh.con.sh/https://github.com/jadehh/pythonTools/releases/download/v1.3.9/PRC
RUN ln -sf /usr/share/zoneinfo/PRC /etc/localtime

## 新建日志文件
RUN mkdir /home/jade
RUN touch /home/jade/test.log

## 安装所需环境

RUN add-apt-repository "deb http://security.ubuntu.com/ubuntu xenial-security main"
RUN apt-get update && apt-get install -y libjasper1 libjasper-dev libgl1-mesa-dev libdc1394-dev   && rm -rf /var/lib/apt/lists/*

## 安装Video Codec SDK
RUN wget https://gh.con.sh/https://github.com/jadehh/opencv/releases/download/4.8.0/Video_Codec_SDK_11.1.5.zip && unzip Video_Codec_SDK_11.1.5.zip && rm Video_Codec_SDK_11.1.5.zip
RUN cp /Video_Codec_SDK_11.1.5/Interface/* /usr/local/cuda/include/
RUN cp /Video_Codec_SDK_11.1.5/Lib/linux/stubs/x86_64/* /usr/local/cuda/lib64/stubs/
RUN ln -sT /usr/local/cuda/lib64/stubs/libnvcuvid.so /usr/lib/x86_64-linux-gnu/libnvcuvid.so.1
RUN ln -sT /usr/local/cuda/lib64/stubs/libnvidia-encode.so /usr/lib/x86_64-linux-gnu/libnvidia-encode.so.1
RUN wget https://gh.con.sh/https://github.com/jadehh/opencv/archive/refs/tags/4.8.0.zip && \
    unzip 4.8.0.zip && rm -r 4.8.0.zip
RUN cd opencv-4.8.0/ && git clone https://gh.con.sh/https://github.com/jadehh/opencv_contrib.git
RUN cd opencv-4.8.0/ && mkdir build && cd build && \
cmake -D WITH_NVCUVID=ON -D OPENCV_ENABLE_NONFREE=ON -D WITH_CUDA=ON  -D CUDA_ARCH_BIN=${CUDA_ARCH_BIN} -D WITH_OPENGL=ON -D BUILD_opencv_cudacodec=ON -D BUILD_opencv_cudalegacy=ON -D OPENCV_EXTRA_MODULES_PATH=/opencv-4.8.0/opencv_contrib/modules/  -D BUILD_opencv_python3=ON  -DCMAKE_LIBRARY_PATH=/usr/local/cuda/lib64/stubs ..
RUN cd opencv-4.8.0/build && make -j${CPU_THERAD_COMPILE}
RUN wget https://gh.con.sh/https://github.com/jadehh/OpencvCapture/releases/download/v0.0.0.4/OpencvCapture && chmod a+x OpencvCapture