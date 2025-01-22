ARG Operation_VERSION
FROM  ${Operation_VERSION}
# image 标签
MAINTAINER jadehh@live.com
##安装字体
ENV LANG=C.UTF-8
ARG PYTHON_VERSION
## 安装Python
RUN apt-get update && apt-get install -y wget  build-essential zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev libsqlite3-dev wget libbz2-dev && rm -rf /var/lib/apt/lists/*
RUN wget https://www.python.org/ftp/python/${PYTHON_VERSION}/Python-${PYTHON_VERSION}.tgz && tar -xf Python-${PYTHON_VERSION}.tgz && rm Python-${PYTHON_VERSION}.tgz && cd  Python-${PYTHON_VERSION}/ && ./configure --enable-shared && make -j $(nproc) &&  make altinstall && rm -r /Python-${PYTHON_VERSION}/
RUN mv /usr/local/lib/libpython* /usr/lib/x86_64-linux-gnu/
RUN  ln -sT /usr/local/bin/python${PYTHON_VERSION%.*} /usr/bin/python && ln -sT /usr/local/bin/pip${PYTHON_VERSION%.*} /usr/bin/pip && pip install  --upgrade pip



