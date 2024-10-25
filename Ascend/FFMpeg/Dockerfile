# Release环境
FROM jadehh/ubuntu:aarch-18.04



RUN apt-get update && apt-get install -y wget unzip && apt-get install -y build-essential && apt-get install -y openssh-server && apt-get install -y htop  && apt-get install -y sudo  && apt-get install -y ntpdate  && rm -rf /var/lib/apt/lists/*



## 设置中文环境
ENV LANG=C.UTF-8

## 安装推理引擎
RUN wget https://gh.con.sh/https://github.com/jadehh/samples/releases/download/v1.0.7/Ascend-cann-nnrt_6.0.0.alpha001_linux-aarch64.run
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


## 下载Ascend FFMpeg

RUN wget https://gh.con.sh/https://github.com/jadehh/AscendDemo/releases/download/1.0.1/Ascendffmpeg.zip && unzip Ascendffmpeg.zip && rm Ascendffmpeg.zip

## 编译FFMpeg

RUN cd Ascendffmpeg && chmod a+x



RUN echo "root:samples@123" | chpasswd
# 添加用户
RUN useradd -ms /bin/bash samples
# 设置密码
RUN echo "samples:samples@123" | chpasswd
## 添加 samples sudo
RUN echo 'samples    ALL=(ALL:ALL) ALL' >> /etc/sudoers
RUN mkdir /var/run/sshd
RUN echo 'Port 2222' >> /etc/ssh/sshd_config
RUN echo 'ListenAddress 0.0.0.0' >> /etc/ssh/sshd_config
RUN echo 'PermitUserEnvironment yes' >> /etc/ssh/sshd_config
RUN echo 'export  LD_LIBRARY_PATH=LD_LIBRARY_PATH:/home/data/miniD/driver/lib64:/usr/local/Ascend/nnrt/latest/lib64:' >> /home/samples/.bashrc
CMD ["/usr/sbin/sshd", "-D"]



