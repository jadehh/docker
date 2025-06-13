# Tensorrt Runtime
FROM  jadehh/opencv-cuda:11.6.2-arch8.6-runtime-py3.8
ARG PYTHON_VERSION
# image 标签
MAINTAINER jadehh@live.com

## 安装Python环境
RUN apt-get update && apt install -y build-essential zlib1g-dev libncurses5-dev \
libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev \
libbz2-dev liblzma-dev tk-dev libsqlite3-dev  && rm -rf /var/lib/apt/lists/*

## 安装Python
RUN wget https://www.python.org/ftp/python/${PYTHON_VERSION}/Python-${PYTHON_VERSION}.tgz && tar -xf Python-${PYTHON_VERSION}.tgz && rm Python-${PYTHON_VERSION}.tgz && cd  Python-${PYTHON_VERSION}/ && ./configure --enable-shared && make -j $(nproc) &&  make altinstall && rm -r /Python-${PYTHON_VERSION}/
RUN mv /usr/local/lib/libpython${PYTHON_VERSION%.*}.so.1.0 /usr/lib/x86_64-linux-gnu/
RUN ln -sT /usr/lib/x86_64-linux-gnu/libpython${PYTHON_VERSION%.*}.so.1.0 /usr/lib/x86_64-linux-gnu/libpython${PYTHON_VERSION%.*}.so
RUN ln -sT /usr/lib/x86_64-linux-gnu/libpython${PYTHON_VERSION%.*}.so.1.0 /usr/lib/x86_64-linux-gnu/libpython${PYTHON_VERSION%%.*}.so
RUN ln -sT /usr/local/bin/python${PYTHON_VERSION%.*} /usr/local/bin/python && ln -sT /usr/local/bin/pip${PYTHON_VERSION%.*} /usr/local/bin/pip
RUN ln -sT  /usr/local/opencv/cv2.cpython-38-x86_64-linux-gnu.so  /usr/local/lib/python${PYTHON_VERSION%.*}/site-packages/cv2.cpython-38-x86_64-linux-gnu.so
RUN pip install cuda-python==12.2.0 && pip install numpy && rm -rf ~/.cache/pip

# 添加 NVIDIA TensorRT 存储库
RUN wget -q  https://developer.download.nvidia.com/compute/machine-learning/tensorrt/10.6.0/tars/TensorRT-10.6.0.26.Linux.x86_64-gnu.cuda-11.8.tar.gz && tar -xvf  TensorRT-10.6.0.26.Linux.x86_64-gnu.cuda-11.8.tar.gz && rm -r TensorRT-10.6.0.26.Linux.x86_64-gnu.cuda-11.8.tar.gz && mv /TensorRT-10.6.0.26/ /usr/local/tensorrt
RUN pip install /usr/local/tensorrt/python/tensorrt-10.6.0-cp38-none-linux_x86_64.whl

## 设置动态库搜索路径（Linux容器）
ENV LD_LIBRARY_PATH="/usr/local/tensorrt/lib/:$LD_LIBRARY_PATH"
## 设置可执行文件搜索路径
ENV PATH="/usr/local/tensorrt/bin:$PATH"


