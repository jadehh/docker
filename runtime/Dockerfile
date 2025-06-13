# Tensorrt Runtime
FROM  jadehh/opencv-cuda:11.6.2-arch8.6-runtime-py3.8
# image 标签
MAINTAINER jadehh@live.com

# 安装加密狗驱动
RUN  wget https://github.com/jadehh/pythonTools/releases/download/JadeV1.9.7/aksusbd_8.51-1_amd64.deb && dpkg -i aksusbd_8.51-1_amd64.deb && rm aksusbd_8.51-1_amd64.deb
RUN  wget https://github.com/jadehh/pythonTools/releases/download/JadeV1.9.7/hasplm.ini && cp hasplm.ini /etc/hasplm/ && rm hasplm.ini

# 安装Tensorrt环境
#  https://developer.download.nvidia.com/compute/machine-learning/tensorrt/10.6.0/tars/TensorRT-10.6.0.26.Linux.x86_64-gnu.cuda-11.8.tar.gz
RUN mkdir /usr/local/tensorrt/ && mkdir /usr/local/tensorrt/targets && mkdir /usr/local/tensorrt/targets/x86_64-linux-gnu && mkdir /usr/local/tensorrt/targets/x86_64-linux-gnu/lib/
RUN wget -q  http://192.168.40.215:8081/H%3A/%E8%BD%AF%E4%BB%B6/TensorRT-10.6.0.26.Linux.x86_64-gnu.cuda-11.8.tar.gz && \
    tar -xvf  TensorRT-10.6.0.26.Linux.x86_64-gnu.cuda-11.8.tar.gz && rm -r TensorRT-10.6.0.26.Linux.x86_64-gnu.cuda-11.8.tar.gz && \
    mv /TensorRT-10.6.0.26/targets/x86_64-linux-gnu/lib/libnvinfer.so* /usr/local/tensorrt/targets/x86_64-linux-gnu/lib/ && \
    mv /TensorRT-10.6.0.26/targets/x86_64-linux-gnu/lib/libnvinfer_plugin.so* /usr/local/tensorrt/targets/x86_64-linux-gnu/lib/ && \
    mv /TensorRT-10.6.0.26/targets/x86_64-linux-gnu/lib/libnvonnxparser.so* /usr/local/tensorrt/targets/x86_64-linux-gnu/lib/ && \
    ln -s /usr/local/tensorrt/targets/x86_64-linux-gnu/lib  /usr/local/tensorrt/lib  && \
    mv /TensorRT-10.6.0.26/python/tensorrt-10.6.0-cp38-none-linux_x86_64.whl /TensorRT-10.6.0.26/python/tensorrt-10.6.0-cp38-none-linux_x86_64.tgz && \
    unzip /TensorRT-10.6.0.26/python/tensorrt-10.6.0-cp38-none-linux_x86_64.tgz && \
    rm  /TensorRT-10.6.0.26/python/tensorrt-10.6.0-cp38-none-linux_x86_64.tgz && \
    rm -r /TensorRT-10.6.0.26 && \
    mv tensorrt* /usr/local/site-packages/

# 设置动态库搜索路径（Linux容器）
ENV LD_LIBRARY_PATH="/usr/local/tensorrt/lib/:$LD_LIBRARY_PATH"

# 安装SamplesTensorrtOps
RUN wget https://github.com/jadehh/pythonTools/releases/download/JadeV2.3.9/samplesTensorrtOps.so && mv samplesTensorrtOps.so /usr/local/site-packages/

# 安装cuda-python

RUN wget https://files.pythonhosted.org/packages/e1/48/1f585f258f82399231bccad3c510d772861ee465cf67100101b2b2f4dd08/cuda_python-12.2.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl && \
    mv cuda_python-12.2.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl cuda_python-12.2.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.tgz && \
    unzip cuda_python-12.2.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.tgz && \
    rm  /cuda_python-12.2.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.tgz && \
    mv cuda* /usr/local/site-packages/
