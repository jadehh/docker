# Ascend-infer开发环境
FROM  ubuntu:18.04
# image 标签
MAINTAINER jadehh@live.com
## 安装wget
RUN apt-get update
RUN apt-get install -y wget unzip

## 安装字体
RUN mkdir /usr/share/fonts
RUN wget -P /usr/share/fonts/ https://gh.con.sh/https://github.com/jadehh/pythonTools/releases/download/v1.3.9/simhei.ttf

## 解决时间问题
RUN mkdir /usr/share/zoneinfo/
RUN wget -P /usr/share/zoneinfo/ https://gh.con.sh/https://github.com/jadehh/pythonTools/releases/download/v1.3.9/PRC
RUN ln -sf /usr/share/zoneinfo/PRC /etc/localtime

## 设置中文环境
ENV LANG=C.UTF-8


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



RUN echo "更新下载地址"
## 下载模型文件
RUN mkdir ContainerOCR
RUN wget https://gh.con.sh/https://github.com/jadehh/jadehh_file/releases/download/Container_NpuV1.0.1/models_en.zip
RUN unzip models_en.zip && rm -r models_en.zip && mv models_en/ /ContainerOCR/ && rm -r /ContainerOCR/models_en/onnx_models/ && rm -r /ContainerOCR/models_en/rknn_models/

## 下载箱号识别服务
RUN wget https://gh.con.sh/https://github.com/jadehh/jadehh_file/releases/download/Container_NpuV1.0.1/conta_ocr-ascend.zip
RUN unzip conta_ocr-ascend.zip && rm  conta_ocr-ascend.zip && mv conta_ocr /ContainerOCR/

## 下载箱号服务

RUN wget https://gh.con.sh/https://github.com/jadehh/jadehh_file/releases/download/Container_NpuV1.0.1/conta_service-ascend.zip
RUN unzip conta_service-ascend.zip && rm  conta_service-ascend.zip && mv conta_service /ContainerOCR/

### 下载配置文件
RUN echo  "更新下载配置文件....."
RUN mkdir /ContainerOCR/config/
#RUN wget https://gh.con.sh/https://github.com/jadehh/jadehh_file/releases/download/Container_NpuV1.0.1/config.ini
#RUN mv config.ini /ContainerOCR/config/

RUN echo  "更新下载lib包........"

RUN wget https://gh.con.sh/https://github.com/jadehh/jadehh_file/releases/download/Container_NpuV1.0.1/conta_ocr_aarch64_lib64.zip
RUN unzip conta_ocr_aarch64_lib64.zip && rm conta_ocr_aarch64_lib64.zip && mv conta_ocr_lib64 /ContainerOCR/


RUN wget https://gh.con.sh/https://github.com/jadehh/jadehh_file/releases/download/Container_NpuV1.0.1/conta_service_aarch64_lib64.zip
RUN unzip conta_service_aarch64_lib64.zip && rm  conta_service_aarch64_lib64.zip && mv conta_service_lib64 /ContainerOCR/




ENV ModelType="ascend"
ENV WSPort="8001"
ENV PlatePort="9001"
ENV ContaDetModelPath="models_en/om_models/ContaDetModels/2022-12-01/model_en.om"
ENV ContaDetThreshold="0.6"


ENV FrontCameraIP="192.168.29.182"
ENV FrontCameraUserName="admin"
ENV FrontCameraPasswd="samples123"

ENV LeftCameraIP="192.168.29.181"
ENV LeftCameraUserName="admin"
ENV LeftCameraPasswd="samples123"

ENV BackCameraIP="192.168.29.180"
ENV BackCameraUserName="admin"
ENV BackCameraPasswd="samples123"


ENV DetModelPath="models_en/om_models/TextDetModels/2022-08-30/model_en.om"
ENV RecHModelPath="models_en/om_models/OCRModels/OCRHModels/2022-10-09/model_en.om"
ENV RecVModelPath="models_en/om_models/OCRModels/OCRVModels/2022-10-09/model_en.om"

WORKDIR /ContainerOCR/
RUN chmod a+x conta_service && chmod a+x conta_ocr

RUN echo "./conta_service \
    --model_type $ModelType \
    --ws_port $WSPort \
    --plate_port $PlatePort \
    --model_path $ContaDetModelPath \
    --threshold $ContaDetThreshold &" > run.sh

RUN echo "./conta_ocr \
    --model_type $ModelType \
    --video_path rtsp://$FrontCameraUserName:$FrontCameraPasswd@$FrontCameraIP/h264/ch1/main/av_stream \
    --camera_type front \
    --det_model_path $DetModelPath \
    --rec_h_model_path $RecHModelPath \
    --rec_v_model_path $RecVModelPath &" >> run.sh

RUN echo "./conta_ocr \
    --model_type $ModelType \
    --video_path rtsp://$BackCameraUserName:$BackCameraPasswd@$BackCameraIP/h264/ch1/main/av_stream \
    --camera_type back \
    --det_model_path $DetModelPath \
    --rec_h_model_path $RecHModelPath \
    --rec_v_model_path $RecVModelPath &" >> run.sh

RUN echo "./conta_ocr \
    --model_type $ModelType \
    --video_path rtsp://$LeftCameraUserName:$LeftCameraPasswd@$LeftCameraIP/h264/ch1/main/av_stream \
    --camera_type left \
    --det_model_path $DetModelPath \
    --rec_h_model_path $RecHModelPath \
    --rec_v_model_path $RecVModelPath &" >> run.sh

RUN touch /usr/local/info.log



## 清除缓存
#RUN apt-get purge -y wget unzip
#RUN apt-get clean