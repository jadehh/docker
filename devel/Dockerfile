FROM jadehh/opencv-cuda:11.6.2-arch8.6-runtime-py3.8
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y cmake git wget  && rm -rf /var/lib/apt/lists/*
RUN ln -s /usr/lib/x86_64-linux-gnu/libcudnn.so.8.9.6  /usr/lib/x86_64-linux-gnu/libcudnn.so && ln -s /usr/local/cuda/lib64/libcublas.so.11.11.3.6 /usr/local/cuda/lib64/libcublas.so
ENV LD_LIBRARY_PATH=/usr/local/cuda/lib64:/usr/local/cuda-11.8/targets/x86_64-linux/lib/:$LD_LIBRARY_PATH
# 添加 NVIDIA TensorRT 存储库
#  https://developer.nvidia.com/downloads/compute/machine-learning/tensorrt/10.6.0/tars/TensorRT-10.6.0.26.Linux.x86_64-gnu.cuda-11.8.tar.gz
RUN wget -q   http://192.168.40.215:8081/H%3A/%E8%BD%AF%E4%BB%B6/TensorRT-10.6.0.26.Linux.x86_64-gnu.cuda-11.8.tar.gz  && tar -xvf  TensorRT-10.6.0.26.Linux.x86_64-gnu.cuda-11.8.tar.gz && rm -r TensorRT-10.6.0.26.Linux.x86_64-gnu.cuda-11.8.tar.gz && mv /TensorRT-10.6.0.26/ /usr/local/tensortrt
# 设置动态库搜索路径（Linux容器）
ENV LD_LIBRARY_PATH="/usr/local/tensortrt/lib/:$LD_LIBRARY_PATH"
# 设置可执行文件搜索路径
ENV PATH="/usr/local/tensortrt/bin:$PATH"