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



RUN if [ ${CUDA_VERSION} = "11.6.2" ];\
    then \
    wget http://mirrors.bfsu.edu.cn/pypi/web/packages/c4/c7/f19c971876a69cc834af7d5951092e4e48ed625c364e179148e122ed6d8f/onnxruntime_gpu-1.15.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl  --no-check-certificate && \
    mv onnxruntime_gpu-1.15.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl onnxruntime_gpu-1.15.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.tgz && \
    unzip onnxruntime_gpu-1.15.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.tgz && \
    rm  onnxruntime_gpu-1.15.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.tgz && \
    mv onnxruntime /usr/local/site-packages/ ; \
    fi
RUN if [ ${CUDA_VERSION} = "10.2" ];\
    then \
    wget http://mirrors.bfsu.edu.cn/pypi/web/packages/3e/52/6e614b800b9e6c6c0d77623569b564ac7eb627e13142d85bcebdbd5b8a92/onnxruntime_gpu-1.5.1-cp38-cp38-manylinux2014_x86_64.whl  --no-check-certificate && \
    mv onnxruntime_gpu-1.5.1-cp38-cp38-manylinux2014_x86_64.whl onnxruntime_gpu-1.5.1-cp38-cp38-manylinux2014_x86_64.tgz && \
    unzip onnxruntime_gpu-1.5.1-cp38-cp38-manylinux2014_x86_64.tgz && \
    rm   onnxruntime_gpu-1.5.1-cp38-cp38-manylinux2014_x86_64.tgz && \
    mv onnxruntime /usr/local/site-packages/ ; \
    fi
RUN echo "结束"