# 使用基础镜像
FROM nvidia/cuda:11.8.0-cudnn8-devel-ubuntu22.04
# 设置环境变量避免交互式提示
ENV DEBIAN_FRONTEND=noninteractive

# 安装系统依赖
RUN apt-get update && apt-get install -y wget unzip  git  cmake build-essential && apt-get clean && rm -rf /var/lib/apt/lists/*

# 安装Opencv依赖
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    autoconf \
    libtool \
    libgtk2.0-dev \
    libavcodec-dev \
    libavformat-dev \
    libswscale-dev \
    libv4l-dev \
    libjpeg-dev \
    libpng-dev \
    libtiff-dev \
    libopenjp2-7-dev \
    libopenexr-dev \
    libtbb2 \
    libtbb-dev \
    libdc1394-dev \
    libgtk-3-dev \
    gfortran && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# 软件连CUDA环境
RUN ln -sT /usr/local/cuda/lib64/stubs/libnvcuvid.so /usr/lib/x86_64-linux-gnu/libnvcuvid.so.1 && ln -sT /usr/local/cuda/lib64/stubs/libnvidia-encode.so /usr/lib/x86_64-linux-gnu/libnvidia-encode.so.1

### 安装Video Codec SDK
RUN wget https://github.com/jadehh/opencv/releases/download/4.8.0/Video_Codec_SDK_11.6.2.zip && unzip Video_Codec_SDK_11.6.2.zip && rm Video_Codec_SDK_11.6.2.zip &&  mv /Video_Codec_SDK_11.6.2/Interface/* /usr/local/cuda/include/ && mv /Video_Codec_SDK_11.6.2/Lib/linux/stubs/x86_64/* /usr/local/cuda/lib64/stubs/ && rm -r /Video_Codec_SDK_11.6.2
# 安装opencv
#####
#
RUN wget https://github.com/jadehh/opencv/archive/refs/tags/4.8.0.zip && unzip 4.8.0.zip && rm -r 4.8.0.zip && \
    cd opencv-4.8.0/ && git clone https://github.com/jadehh/opencv_contrib.git && mkdir build && cd build && \
    cmake -D CMAKE_BUILD_TYPE=RELEASE  \
          -D CMAKE_INSTALL_PREFIX=/usr/local  \
          -D WITH_NVCUVID=ON \
          -D OPENCV_ENABLE_NONFREE=ON  \
          -D WITH_CUDA=ON  \
          -D CUDA_ARCH_BIN="7.5;8.6;8.9" \
          -D WITH_OPENGL=ON \
          -D BUILD_opencv_cudacodec=ON \
          -D BUILD_opencv_cudalegacy=ON \
          -D OPENCV_EXTRA_MODULES_PATH=/opencv-4.8.0/opencv_contrib/modules/ \
          -D CMAKE_LIBRARY_PATH=/usr/local/cuda/lib64/stubs .. && \
    make -j $(nproc) && make install  && rm -r /opencv-4.8.0/

# 安装Paddle环境
RUN git clone https://github.com/paddlepaddle/Paddle && cd Paddle && mkdir build && cd build && \
    cmake -DFLUID_INFERENCE_INSTALL_DIR=/usr/local/paddle \
      -DCMAKE_BUILD_TYPE=Release \
      -DWITH_PYTHON=OFF \
      -DWITH_MKL=OFF \
      -DWITH_GPU=ON  \
      -DON_INFER=ON \
      -DWITH_NCCL=OFF .. & \
     make -j$(nproc) && make install && rm -r /Paddle/