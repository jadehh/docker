# Opencv开发环境
ARG CUDA_VERSION
ARG CUDNN_VERSION
ARG CUDA_ARCH_BIN
FROM  nvidia/cuda:${CUDA_VERSION}-cudnn${CUDNN_VERSION}-devel-ubuntu18.04
ARG CUDA_VERSION
ARG CUDNN_VERSION
ARG CUDA_ARCH_BIN
ARG PYTHON_VERSION
# image 标签
MAINTAINER jadehh@live.com
## 设置语言
ENV LANG=C.UTF-8
RUN echo "CUDA版本为:${CUDA_VERSION}"
RUN echo "CUDNN版本为:${CUDNN_VERSION}"
RUN echo "计算能力为:${CUDA_ARCH_BIN}"

## 换源
RUN rm -r /etc/apt/sources.list
# 默认注释了源码仓库，如有需要可自行取消注释
RUN echo "deb https://mirrors.ustc.edu.cn/ubuntu/ bionic main restricted universe multiverse" > /etc/apt/sources.list && \
    echo "deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-security main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-security main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse" >> /etc/apt/sources.list

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys A4B469963BF863CC
RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y wget unzip  cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev  libswscale-dev libopenblas-dev  libgstreamer-plugins-base1.0-dev libgstreamer1.0-dev  libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev  software-properties-common  build-essential zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev libsqlite3-dev  libbz2-dev  && rm -rf /var/lib/apt/lists/*

## 安装Python
RUN wget https://www.python.org/ftp/python/${PYTHON_VERSION}/Python-${PYTHON_VERSION}.tgz && tar -xf Python-${PYTHON_VERSION}.tgz && rm Python-${PYTHON_VERSION}.tgz && cd  Python-${PYTHON_VERSION}/ && ./configure --enable-shared && make -j $(nproc) &&  make altinstall && rm -r /Python-${PYTHON_VERSION}/
RUN mv /usr/local/lib/libpython${PYTHON_VERSION%.*}.so.1.0 /usr/lib/x86_64-linux-gnu/
RUN ln -sT /usr/lib/x86_64-linux-gnu/libpython${PYTHON_VERSION%.*}.so.1.0 /usr/lib/x86_64-linux-gnu/libpython${PYTHON_VERSION%.*}.so
RUN ln -sT /usr/lib/x86_64-linux-gnu/libpython${PYTHON_VERSION%.*}.so.1.0 /usr/lib/x86_64-linux-gnu/libpython${PYTHON_VERSION%%.*}.so
RUN mkdir /root/.pip/
RUN touch /root/.pip/pip.conf
RUN echo "[global]" >> /root/.pip/pip.conf
RUN echo "index-url = http://mirrors.bfsu.edu.cn/pypi/web/simple" >> /root/.pip/pip.conf
RUN echo "trusted-host = mirrors.bfsu.edu.cn" >> /root/.pip/pip.conf
RUN pip${PYTHON_VERSION%.*} install numpy

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
RUN apt-get update && apt-get install -y  libdc1394-22-dev  libjasper1 libjasper-dev libgl1-mesa-dev && rm -rf /var/lib/apt/lists/*


### 安装Video Codec SDK
RUN wget https://gh.con.sh/https://github.com/jadehh/opencv/releases/download/4.8.0/Video_Codec_SDK_11.6.2.zip && unzip Video_Codec_SDK_11.6.2.zip && rm Video_Codec_SDK_11.6.2.zip &&  mv /Video_Codec_SDK_11.6.2/Interface/* /usr/local/cuda/include/ && mv /Video_Codec_SDK_11.6.2/Lib/linux/stubs/x86_64/* /usr/local/cuda/lib64/stubs/ && rm -r /Video_Codec_SDK_11.6.2
RUN ln -sT /usr/local/cuda/lib64/stubs/libnvcuvid.so /usr/lib/x86_64-linux-gnu/libnvcuvid.so.1
RUN ln -sT /usr/local/cuda/lib64/stubs/libnvidia-encode.so /usr/lib/x86_64-linux-gnu/libnvidia-encode.so.1
RUN wget https://gh.con.sh/https://github.com/jadehh/opencv/archive/refs/tags/4.8.0.zip && \
    unzip 4.8.0.zip && rm -r 4.8.0.zip
RUN cd opencv-4.8.0/ && git clone https://gh.con.sh/https://github.com/jadehh/opencv_contrib.git
RUN cd opencv-4.8.0/ && mkdir build && cd build && \
cmake -D WITH_NVCUVID=ON -D OPENCV_ENABLE_NONFREE=ON -D WITH_CUDA=ON  -D CUDA_ARCH_BIN=${CUDA_ARCH_BIN} -D WITH_OPENGL=ON -D BUILD_opencv_cudacodec=ON -D BUILD_opencv_cudalegacy=ON -D OPENCV_EXTRA_MODULES_PATH=/opencv-4.8.0/opencv_contrib/modules/  -D BUILD_opencv_python3=ON -D PYTHON3_EXECUTABLE=/usr/local/bin/python${PYTHON_VERSION%.*} -D PYTHON3_LIBRARY=/usr/lib/x86_64-linux-gnu/libpython${PYTHON_VERSION%.*}.so  -D PYTHON3_NUMPY_INCLUDE_DIRS=/usr/local/lib/python${PYTHON_VERSION%.*}/site-packages/numpy/core/include/   -DCMAKE_LIBRARY_PATH=/usr/local/cuda/lib64/stubs ..

RUN cd opencv-4.8.0/build && make -j $(nproc)
## 去除多余输出
RUN if [ "$CUDA_VERSION" = "11.6.2" ];\
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

## 安装numpy
RUN mkdir /usr/local/site-packages
RUN if [ ${PYTHON_VERSION%.*} = "3.10" ];\
    then \
      ## 去除docker容器的输出 \
    wget http://mirrors.bfsu.edu.cn/pypi/web/packages/d0/55/559e6f455a066e12058330377259a106b7fefa41c15dbdb1b71070cec429/numpy-1.25.1-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl && mv numpy-1.25.1-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl numpy.zip && unzip numpy.zip && mv /numpy* /usr/local/site-packages/ && rm -r /usr/local/site-packages/numpy.zip; \
    fi
RUN if [ ${PYTHON_VERSION%.*} = "3.8" ];\
    then \
      ## 去除docker容器的输出 \
    wget https://mirrors.bfsu.edu.cn/pypi/web/packages/98/5d/5738903efe0ecb73e51eb44feafba32bdba2081263d40c5043568ff60faf/numpy-1.24.4-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl && mv numpy-1.24.4-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl numpy.zip && unzip numpy.zip && mv /numpy* /usr/local/site-packages/ && rm -r /usr/local/site-packages/numpy.zip; \
    fi


RUN wget https://gh.con.sh/https://github.com/jadehh/OpencvCapture/releases/download/v0.0.1.8/OpencvCapture-py${PYTHON_VERSION%.*}  && mv  OpencvCapture-py${PYTHON_VERSION%.*} OpencvCapture && chmod a+x OpencvCapture
RUN mkdir /usr/local/opencv
# 拷贝cv2.so的依赖项
RUN wget  https://gh.con.sh/https://github.com/jadehh/LDDTools/releases/download/v0.0.1.4/LDDTools-py${PYTHON_VERSION%.*}&& mv LDDTools-py${PYTHON_VERSION%.*} LDDTools && chmod a+x LDDTools && \
    ./LDDTools -binary_file  /opencv-4.8.0/build/lib/python3/cv2.* -output_dir /usr/local/opencv && rm LDDTools
RUN cp  /opencv-4.8.0/build/lib/python3/cv2.*  /usr/local/opencv
RUN tar -czvf opencv-cuda-${CUDA_VERSION}-cudnn${CUDNN_VERSION}-arch-${CUDA_ARCH_BIN}-py${PYTHON_VERSION%.*}.gz  /usr/local/opencv



