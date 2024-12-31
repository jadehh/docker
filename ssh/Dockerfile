FROM ubuntu:24.04

RUN apt-get update
RUN apt-get install -y wget unzip

## 安装SSH和Sudo命令
RUN apt-get update && apt-get install -y openssh-server && apt-get install -y htop  && apt-get install -y sudo  && apt-get install -y ntpdate  && rm -rf /var/lib/apt/lists/*
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
RUN apt-get update && apt-get install -y python3-pyqt5 python3-pip xarclock
RUN mkdir /home/samples/.pip
RUN echo '[global]' > /home/samples/.pip/pip.conf
RUN echo 'index-url = https://mirrors.ustc.edu.cn/pypi/simple/' >> /home/samples/.pip/pip.conf
CMD ["/usr/sbin/sshd", "-D"]