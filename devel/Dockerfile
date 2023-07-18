# Opencv开发环境
ARG Operation_VERSION
ARG CUDA_VERSION
ARG CUDNN_VERSION
ARG CUDA_ARCH_BIN
FROM  jadehh/opencv-cuda:${CUDA_VERSION}-arch-${CUDA_ARCH_BIN}-opencv4-8-0-runtime-${Operation_VERSION}
ARG Operation_VERSION
ARG CUDA_VERSION
ARG CUDNN_VERSION
ARG CUDA_ARCH_BIN
# image 标签
MAINTAINER jadehh@live.com
## 安装MiniConda3

RUN apt-get update && apt-get install -y python3 python3-pip  && rm -rf /var/lib/apt/lists/*

RUN ln -sT /usr/bin/python3 /usr/bin/python && ln -sT  /usr/bin/pip3 /usr/bin/pip && pip install  --upgrade pip

RUN mkdir /root/.pip/
RUN touch /root/.pip/pip.conf
RUN echo "[global]" >> /root/.pip/pip.conf
RUN echo "index-url = https://mirrors.bfsu.edu.cn/pypi/web/simple" >> /root/.pip/pip.conf
RUN echo "trusted-host = mirrors.bfsu.edu.cn" >> /root/.pip/pip.conf
RUN pip install numpy
RUN if [ "$CUDA_VERSION" == "10.0" ];\
    then \
      ## 去除docker容器的输出 \
    pip install onnxruntime-gpu==1.4;\
    fi

