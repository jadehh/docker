# Ascend-infer开发环境
FROM  ubuntu:18.04
# image 标签
MAINTAINER jadehh@live.com
##安装字体

ENV LANG=C.UTF-8
## 安装 wget vim
RUN apt-get update
RUN apt-get install -y wget

## 安装字体
RUN mkdir /usr/share/fonts
RUN wget -P /usr/share/fonts/ https://gh.con.sh/https://github.com/jadehh/pythonTools/releases/download/v1.3.9/simhei.ttf

## 解决时间问题
RUN mkdir /usr/share/zoneinfo/
RUN wget -P /usr/share/zoneinfo/ https://gh.con.sh/https://github.com/jadehh/pythonTools/releases/download/v1.3.9/PRC
RUN ln -sf /usr/share/zoneinfo/PRC /etc/localtime


## 新建日志文件
RUN mkdir /home/jade
RUN touch /home/jade/test.log


## 清除缓存
RUN apt-get purge -y wget
RUN apt-get clean