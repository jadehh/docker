# ONNX Runtime
FROM  jadehh/opencv-cuda:10.2-arch7.5-runtime-py3.8
# image 标签
MAINTAINER jadehh@live.com

RUN wget https://github.com/jadehh/pythonTools/releases/download/OpencvToolsV1.3.2/onnxruntime_gpu-1.6.0-cp38-cp38-manylinux2014_x86_64.whl  --no-check-certificate && \
    mv onnxruntime_gpu-1.6.0-cp38-cp38-manylinux2014_x86_64.whl onnxruntime_gpu-1.6.0-cp38-cp38-manylinux2014_x86_64.tgz && \
    unzip onnxruntime_gpu-1.6.0-cp38-cp38-manylinux2014_x86_64.tgz && \
    rm  onnxruntime_gpu-1.6.0-cp38-cp38-manylinux2014_x86_64.tgz && \
    mv onnxruntime /usr/local/site-packages/

## 安装加密狗驱动
RUN  wget https://github.com/jadehh/pythonTools/releases/download/JadeV1.9.7/aksusbd_8.51-1_amd64.deb && dpkg -i aksusbd_8.51-1_amd64.deb && rm aksusbd_8.51-1_amd64.deb
RUN  wget https://github.com/jadehh/pythonTools/releases/download/JadeV1.9.7/hasplm.ini && cp hasplm.ini /etc/hasplm/ && rm hasplm.ini
