# Ascend-infer开发环境
ARG Operation_VERSION
ARG CUDA_VERSION
ARG CUDA_ARCH_BIN
FROM jadehh/opencv-cuda:${CUDA_VERSION}-arch-${CUDA_ARCH_BIN}-opencv4-8-0-runtime-${Operation_VERSION}
# image 标签
MAINTAINER jadehh@live.com
RUN apt-get update && apt-get install -y unzip  && rm -rf /var/lib/apt/lists/*

## 安装onnxrutime-gpu
RUN wget https://mirrors.bfsu.edu.cn/pypi/web/packages/4f/fb/8183e839b15edb399cdb8cc9df9bcce62f0339cd8d37800be1c00fb9bd2e/onnxruntime_gpu-1.14.0-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl  --no-check-certificate && \
    mv onnxruntime_gpu-1.14.0-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl onnxruntime_gpu-1.14.0-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.tgz && \
    unzip onnxruntime_gpu-1.14.0-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.tgz && \
    rm  onnxruntime_gpu-1.14.0-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.tgz && \
    mkdir /usr/local/site-packages/ && \
    mv onnxruntime /usr/local/site-packages/

