FROM jadehh/opencv-cuda:11.6.2-arch8.6-devel-py3.8
# 添加 NVIDIA TensorRT 存储库
#  https://developer.nvidia.com/downloads/compute/machine-learning/tensorrt/10.6.0/tars/TensorRT-10.6.0.26.Linux.x86_64-gnu.cuda-11.8.tar.gz
RUN wget -q   http://192.168.40.215:8081/H%3A/%E8%BD%AF%E4%BB%B6/TensorRT-10.6.0.26.Linux.x86_64-gnu.cuda-11.8.tar.gz  && tar -xvf  TensorRT-10.6.0.26.Linux.x86_64-gnu.cuda-11.8.tar.gz && rm -r TensorRT-10.6.0.26.Linux.x86_64-gnu.cuda-11.8.tar.gz && mv /TensorRT-10.6.0.26/ /usr/local/tensorrt
# 设置动态库搜索路径（Linux容器）
ENV LD_LIBRARY_PATH="/usr/local/tensorrt/lib/:$LD_LIBRARY_PATH"
# 设置可执行文件搜索路径
ENV PATH="/usr/local/tensorrt/bin:$PATH"
# 卸载旧版本的Cmake安装新版Cmake
RUN apt-get purge -y cmake && wget https://github.com/Kitware/CMake/releases/download/v3.28.2/cmake-3.28.2.tar.gz && tar -xzvf cmake-3.28.2.tar.gz && cd cmake-3.28.2 && chmod 777 ./configure && ./configure && make -j$(nproc)  &&  make install && rm -r cmake*
RUN update-alternatives --install /usr/bin/cmake cmake /usr/local/bin/cmake 1 --force

# 安装PaddleInference

RUN wget https://paddle-inference-lib.bj.bcebos.com/3.0.0/cxx_c/Linux/GPU/x86-64_gcc11.2_avx_mkl_cuda11.8_cudnn8.9.7-trt8.6.1.6/paddle_inference.tgz
