# 使用基础镜像
FROM nvidia/cuda:11.8.0-cudnn8-runtime-ubuntu22.04
# 设置环境变量避免交互式提示
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y wget unzip  git   libjasper1 libjasper-dev libgl1-mesa-dev libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev  libswscale-dev libopenblas-dev  libgstreamer-plugins-base1.0-dev libgstreamer1.0-dev  libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev  software-properties-common  build-essential zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev libsqlite3-dev  libbz2-dev  && rm -rf /var/lib/apt/lists/*


# 安装新版Cmake
RUN wget https://github.com/Kitware/CMake/releases/download/v3.28.2/cmake-3.28.2.tar.gz && tar -xzvf cmake-3.28.2.tar.gz && cd cmake-3.28.2 && chmod 777 ./configure && ./configure && make -j$(nproc)  &&  make install && rm -r /cmake*
RUN update-alternatives --install /usr/bin/cmake cmake /usr/local/bin/cmake 1 --force

# 安装Opencv
RUN wget https://paddleocr.bj.bcebos.com/libs/opencv/opencv-3.4.7.tar.gz && tar -xf opencv-3.4.7.tar.gz && rm -r opencv-3.4.7.tar.gz && \
    cd opencv-3.4.7 && mkdir build && cd build && \
    cmake .. \
    -DCMAKE_INSTALL_PREFIX=/usr/local/opencv/ \
    -DCMAKE_BUILD_TYPE=Release \
    -DBUILD_SHARED_LIBS=OFF \
    -DWITH_IPP=OFF \
    -DBUILD_IPP_IW=OFF \
    -DWITH_LAPACK=OFF \
    -DWITH_EIGEN=OFF \
    -DCMAKE_INSTALL_LIBDIR=lib64 \
    -DWITH_ZLIB=ON \
    -DBUILD_ZLIB=ON \
    -DWITH_JPEG=ON \
    -DBUILD_JPEG=ON \
    -DWITH_PNG=ON \
    -DBUILD_PNG=ON \
    -DWITH_TIFF=ON \
    -DBUILD_TIFF=ON &&\
    make -j$(nproc) && make install && rm -r /opencv-3.4.7/

# 安装Paddle Inference
RUN wget -q http://192.168.40.215:8081/H%3A/%E8%BD%AF%E4%BB%B6/paddle_inference.tgz && tar -xvf paddle_inference.tgz && rm -r paddle_inference.tgz && mv paddle_inference /usr/local/paddle_inference

