# Devlop环境
FROM jadehh/miniconda3:aarch64-4.9.2



## 安装推理引擎
RUN wget https://ascend-repo.obs.cn-east-2.myhuaweicloud.com/CANN/6.0.0.alpha001/Ascend-cann-nnrt_6.0.0.alpha001_linux-aarch64.run
RUN umask 0022 && \
    groupadd -g 1001 HwHiAiUser && useradd -g HwHiAiUser -d /home/HwHiAiUser -m HwHiAiUser && usermod -u 1001 HwHiAiUser &&\
    chmod +x Ascend-cann-nnrt_6.0.0.alpha001_linux-aarch64.run &&\
    ./Ascend-cann-nnrt_6.0.0.alpha001_linux-aarch64.run --quiet --install && \
     rm Ascend-cann-nnrt_6.0.0.alpha001_linux-aarch64.run

## 设置推理引擎环境变量
ENV ASCEND_NNRT_HOME=/usr/local/Ascend/nnrt/latest/
ENV LD_LIBRARY_PATH=${ASCEND_NNRT_HOME}/lib64:$LD_LIBRARY_PATH
ENV PYTHONPATH=${ASCEND_NNRT_HOME}/python/site-packages:$PYTHONPATH
ENV ASCEND_AICPU_PATH=${ASCEND_NNRT_HOME}
ENV ASCEND_OPP_PATH=${ASCEND_NNRT_HOME}/opp
ENV PYTHONPATH=/home/data/miniD/driver/lib64:$PYTHONPATH
ENV LD_LIBRARY_PATH=/home/data/miniD/driver/lib64:$LD_LIBRARY_PATH


## pip环境设置
RUN pip install opencv-python-headless==4.6.0.66
RUN pip install pyclipper==1.3.0.post4
RUN pip install shapely==2.0rc3
RUN pip install pillow==8.2.0
RUN pip install av==10.0.0
RUN pip install tornado==4.5.1
RUN pip install scipy==1.5.4
RUN pip install spyne==2.13.16
RUN pip install requests==2.26.0
RUN pip install lxml==4.7.1
RUN pip install suds==1.1.2
RUN pip install https://gh.ddlc.top/https://github.com/jadehh/samples/releases/download/v1.0.2/acllite-1.0.2-py3-none-any.whl
RUN pip install https://gh.ddlc.top/https://github.com/jadehh/pythonTools/releases/download/OpencvToolsV1.2.0/opencv_tools-1.2.0-py3-none-any.whl
RUN pip install https://gh.ddlc.top/https://github.com/jadehh/pythonTools/releases/download/JadeV1.5.8/jade-1.5.8-py3-none-any.whl






