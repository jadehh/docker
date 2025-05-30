# ONNX Runtime
FROM  jadehh/opencv-cuda:11.6.2-arch8.6-runtime-py3.8
# image 标签
MAINTAINER jadehh@live.com

RUN wget https://files.pythonhosted.org/packages/dd/1f/6048048c013087ae19faa5c6a56907ae5ff3941ad5652323035962faebba/onnxruntime_gpu-1.18.0-cp38-cp38-manylinux_2_28_x86_64.whl  --no-check-certificate && \
mv onnxruntime_gpu-1.18.0-cp38-cp38-manylinux_2_28_x86_64.whl onnxruntime_gpu-1.18.0-cp38-cp38-manylinux_2_28_x86_64.tgz && \
unzip onnxruntime_gpu-1.18.0-cp38-cp38-manylinux_2_28_x86_64.tgz && \
rm  onnxruntime_gpu-1.18.0-cp38-cp38-manylinux_2_28_x86_64.tgz && \
mv onnxruntime /usr/local/site-packages/

## 安装加密狗驱动
RUN  wget https://github.com/jadehh/pythonTools/releases/download/JadeV1.9.7/aksusbd_8.51-1_amd64.deb && dpkg -i aksusbd_8.51-1_amd64.deb && rm aksusbd_8.51-1_amd64.deb
RUN  wget https://github.com/jadehh/pythonTools/releases/download/JadeV1.9.7/hasplm.ini && cp hasplm.ini /etc/hasplm/ && rm hasplm.ini
