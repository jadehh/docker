# ONNX Runtime
ARG CUDA_VERSION
ARG CUDA_ARCH_BIN
ARG PYTHON_VERSION
FROM  jadehh/opencv-cuda:${CUDA_VERSION}-arch${CUDA_ARCH_BIN}-runtime-py${PYTHON_VERSION}
ARG CUDA_VERSION
ARG CUDNN_VERSION
ARG CUDA_ARCH_BIN
# image 标签
MAINTAINER jadehh@live.com
## 安装onnxrutime-gpu
RUN wget https://mirrors.bfsu.edu.cn/pypi/web/packages/4f/fb/8183e839b15edb399cdb8cc9df9bcce62f0339cd8d37800be1c00fb9bd2e/onnxruntime_gpu-1.14.0-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl  --no-check-certificate && \
    mv onnxruntime_gpu-1.14.0-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl onnxruntime_gpu-1.14.0-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.tgz && \
    unzip onnxruntime_gpu-1.14.0-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.tgz && \
    rm  onnxruntime_gpu-1.14.0-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.tgz && \
    mv onnxruntime /usr/local/site-packages/