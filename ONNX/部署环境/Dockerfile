# Ascend-infer开发环境
FROM  nvidia/cuda:10.0-cudnn7-runtime-ubuntu18.04
# image 标签
MAINTAINER jadehh@live.com
## 换源
RUN rm -r  /etc/apt/sources.list
RUN rm -r  /etc/apt/sources.list.d/*
RUN echo "deb  http://mirrors.aliyun.com/ubuntu/ xenial main" > /etc/apt/sources.list
## 安装wget
RUN apt-get update
RUN apt-get install -y wget libxcb* unzip

## 安装字体
RUN mkdir /usr/share/fonts
RUN wget -P /usr/share/fonts/ https://ghproxy.com/https://github.com/jadehh/pythonTools/releases/download/v1.3.9/simhei.ttf

## 解决时间问题
RUN mkdir /usr/share/zoneinfo/
RUN wget -P /usr/share/zoneinfo/ https://ghproxy.com/https://github.com/jadehh/pythonTools/releases/download/v1.3.9/PRC
RUN ln -sf /usr/share/zoneinfo/PRC /etc/localtime

## 设置中文环境
ENV LANG=C.UTF-8


# 软连接CUDA
RUN ln -s /usr/local/cuda/lib64/libcublas.so.10.0.130 /usr/local/cuda/lib64/libcublas.so
RUN ln -s /usr/local/cuda/lib64/libcudart.so.10.0.130 /usr/local/cuda/lib64/libcudart.so
RUN ln -s /usr/local/cuda/lib64/libcurand.so.10.0.130 /usr/local/cuda/lib64/libcurand.so
RUN ln -s /usr/local/cuda/lib64/libcusolver.so.10.0.130 /usr/local/cuda/lib64/libcusolver.so
RUN ln -s /usr/local/cuda/lib64/libcusparse.so.10.0.130 /usr/local/cuda/lib64/libcusparse.so
RUN ln -s /usr/local/cuda/lib64/libnppc.so.10.0.130 /usr/local/cuda/lib64/libnppc.so
RUN ln -s /usr/local/cuda/lib64/libnppial.so.10.0.130 /usr/local/cuda/lib64/libnppial.so
RUN ln -s /usr/local/cuda/lib64/libnppicc.so.10.0.130 /usr/local/cuda/lib64/libnppicc.so
RUN ln -s /usr/local/cuda/lib64/libnppicom.so.10.0.130 /usr/local/cuda/lib64/libnppicom.so
RUN ln -s /usr/local/cuda/lib64/libnppidei.so.10.0.130 /usr/local/cuda/lib64/libnppidei.so
RUN ln -s /usr/local/cuda/lib64/libnppif.so.10.0.130 /usr/local/cuda/lib64/libnppif.so
RUN ln -s /usr/local/cuda/lib64/libnppig.so.10.0.130 /usr/local/cuda/lib64/libnppig.so
RUN ln -s /usr/local/cuda/lib64/libnppim.so.10.0.130 /usr/local/cuda/lib64/libnppim.so
RUN ln -s /usr/local/cuda/lib64/libnppist.so.10.0.130 /usr/local/cuda/lib64/libnppist.so
RUN ln -s /usr/local/cuda/lib64/libnppisu.so.10.0.130 /usr/local/cuda/lib64/libnppisu.so
RUN ln -s /usr/local/cuda/lib64/libnppitc.so.10.0.130 /usr/local/cuda/lib64/libnppitc.so
RUN ln -s /usr/local/cuda/lib64/libnpps.so.10.0.130 /usr/local/cuda/lib64/libnpps.so
RUN ln -s /usr/local/cuda/lib64/libnvblas.so.10.0.130 /usr/local/cuda/lib64/libnvblas.so
RUN ln -s /usr/local/cuda/lib64/libnvgraph.so.10.0.130 /usr/local/cuda/lib64/libnvgraph.so
RUN ln -s /usr/local/cuda/lib64/libnvjpeg.so.10.0.130 /usr/local/cuda/lib64/libnvjpeg.so
RUN ln -s /usr/local/cuda/lib64/libnvrtc.so.10.0.130 /usr/local/cuda/lib64/libnvrtc.so
## cudnn安装
RUN wget https://ghproxy.com/https://github.com/jadehh/jadehh_file/releases/download/Container_NpuV1.0.1/cudnn-7.6.4.tar
RUN tar -xvf cudnn-7.6.4.tar
RUN cp cudnn/libcudnn.so.7.6.4 /usr/local/cuda/lib64
RUN ln -s /usr/local/cuda/lib64/libcudnn.so.7.6.4 /usr/local/cuda/lib64/libcudnn.so
RUN rm cudnn-7.6.4.tar && rm -r cudnn


## 安装onnxrutime-gpu
RUN wget https://mirrors.bfsu.edu.cn/pypi/web/packages/4d/86/b6b4b33e0888f1f3da04ba265fbfc2f2587d04071c790a9503e8c48b4fc3/onnxruntime_gpu-1.1.0-cp36-cp36m-manylinux2010_x86_64.whl  --no-check-certificate
RUN mv onnxruntime_gpu-1.1.0-cp36-cp36m-manylinux2010_x86_64.whl onnxruntime_gpu-1.1.0-cp36-cp36m-manylinux2010_x86_64.tgz
RUN unzip onnxruntime_gpu-1.1.0-cp36-cp36m-manylinux2010_x86_64.tgz
RUN rm  onnxruntime_gpu-1.1.0-cp36-cp36m-manylinux2010_x86_64.tgz
RUN mkdir /usr/local/site-packages/
RUN mv onnxruntime /usr/local/site-packages/
RUN rm -r onnxruntime_gpu-1.1.0.dist-info

## 安装opencv-python
RUN wget https://mirrors.bfsu.edu.cn/pypi/web/packages/35/7b/628da8b9f91342432a9432d900d5e2771c387969430e7d4a513dc6dd7804/opencv_python_headless-4.4.0.40-cp36-cp36m-manylinux2014_x86_64.whl --no-check-certificate
RUN mv opencv_python_headless-4.4.0.40-cp36-cp36m-manylinux2014_x86_64.whl opencv_python_headless-4.4.0.40-cp36-cp36m-manylinux2014_x86_64.zip
RUN unzip opencv_python_headless-4.4.0.40-cp36-cp36m-manylinux2014_x86_64.zip && rm opencv_python_headless-4.4.0.40-cp36-cp36m-manylinux2014_x86_64.zip
RUN mv cv2/ /usr/local/site-packages/
RUN rm -r opencv_python_headless-4.4.0.40.dist-info
RUN cp opencv_python_headless.libs/* /usr/lib/x86_64-linux-gnu/ && rm -r opencv_python_headless.libs
RUN mkdir /home/jade
RUN touch /home/jade/test.log
RUN apt-get purge -y wget unzip
RUN apt-get clean

