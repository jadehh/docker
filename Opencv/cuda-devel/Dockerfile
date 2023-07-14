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
RUN apt-get update
RUN apt-get install -y wget   unzip  cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev  libswscale-dev libopenblas-dev  libgstreamer-plugins-base1.0-dev libgstreamer1.0-dev  libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev  software-properties-common  python3-dev python3-numpy   && rm -rf /var/lib/apt/lists/*



## 安装字体
RUN wget -P /usr/share/fonts/ https://gh.con.sh/https://github.com/jadehh/pythonTools/releases/download/v1.3.9/simhei.ttf

## 解决时间问题
RUN mkdir /usr/share/zoneinfo/
RUN wget -P /usr/share/zoneinfo/ https://gh.con.sh/https://github.com/jadehh/pythonTools/releases/download/v1.3.9/PRC
RUN ln -sf /usr/share/zoneinfo/PRC /etc/localtime

## 新建日志文件
RUN mkdir /home/jade
RUN touch /home/jade/test.log

### 安装所需环境

RUN add-apt-repository "deb http://security.ubuntu.com/ubuntu xenial-security main"
RUN apt-get update && apt-get install -y libjasper1 libjasper-dev libgl1-mesa-dev && rm -rf /var/lib/apt/lists/*
RUN if [ "$Operation_VERSION" = "ubuntu18.04" ];\
    then \
    apt-get update && apt-get install -y libdc1394-22-dev && rm -rf /var/lib/apt/lists/*; \
    fi

RUN if [ "$Operation_VERSION" = "ubuntu20.04" ];\
    then \
     apt-get update && apt-get install -y libdc1394-dev && rm -rf /var/lib/apt/lists/*; \
    fi

### 安装Video Codec SDK
RUN wget https://gh.con.sh/https://github.com/jadehh/opencv/releases/download/4.8.0/Video_Codec_SDK_11.6.2.zip && unzip Video_Codec_SDK_11.6.2.zip && rm Video_Codec_SDK_11.6.2.zip &&  mv /Video_Codec_SDK_11.6.2/Interface/* /usr/local/cuda/include/ && mv /Video_Codec_SDK_11.6.2/Lib/linux/stubs/x86_64/* /usr/local/cuda/lib64/stubs/ && rm -r /Video_Codec_SDK_11.6.2
RUN ln -sT /usr/local/cuda/lib64/stubs/libnvcuvid.so /usr/lib/x86_64-linux-gnu/libnvcuvid.so.1
RUN ln -sT /usr/local/cuda/lib64/stubs/libnvidia-encode.so /usr/lib/x86_64-linux-gnu/libnvidia-encode.so.1
RUN wget https://gh.con.sh/https://github.com/jadehh/opencv/archive/refs/tags/4.8.0.zip && \
    unzip 4.8.0.zip && rm -r 4.8.0.zip
RUN cd opencv-4.8.0/ && git clone https://gh.con.sh/https://github.com/jadehh/opencv_contrib.git
RUN cd opencv-4.8.0/ && mkdir build && cd build && \
cmake -D WITH_NVCUVID=ON -D OPENCV_ENABLE_NONFREE=ON -D WITH_CUDA=ON  -D CUDA_ARCH_BIN=${CUDA_ARCH_BIN} -D WITH_OPENGL=ON -D BUILD_opencv_cudacodec=ON -D BUILD_opencv_cudalegacy=ON -D OPENCV_EXTRA_MODULES_PATH=/opencv-4.8.0/opencv_contrib/modules/  -D BUILD_opencv_python3=ON  -DCMAKE_LIBRARY_PATH=/usr/local/cuda/lib64/stubs ..

RUN cd opencv-4.8.0/build && make -j${CPU_THERAD_COMPILE}
RUN wget https://gh.con.sh/https://github.com/jadehh/OpencvCapture/releases/download/v0.0.0.8/OpencvCapture-${Operation_VERSION} && chmod a+x OpencvCapture-${Operation_VERSION} && mv  OpencvCapture-${Operation_VERSION} OpencvCapture
RUN mkdir /usr/local/opencv
## 拷贝cv2.so的依赖项
RUN wget  https://gh.con.sh/https://github.com/jadehh/LDDTools/releases/download/v0.0.0.9/LDDTools-${Operation_VERSION} && mv LDDTools-${Operation_VERSION} LDDTools && chmod a+x LDDTools && \
    ./LDDTools -binary_file  /opencv-4.8.0/build/lib/python3/cv2.* -output_dir /usr/local/opencv && rm LDDTools
RUN cp  /opencv-4.8.0/build/lib/python3/cv2.*  /usr/local/opencv
RUN tar -czvf opencv-cuda-${CUDA_VERSION}-cudnn${CUDNN_VERSION}-arch-${CUDA_ARCH_BIN}-${Operation_VERSION}.tar.gz  /usr/local/opencv



