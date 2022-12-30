## Ascend部署环境

### 构建Image

```bash
docker build -t jadehh/ascend-infer:v1.0.2 .
```

### 下载config文件

```bash
cd /tmp
wget https://gh.con.sh/https://github.com/jadehh/jadehh_file/releases/download/Container_NpuV1.0.1/config.ini

```

### 或者自定义config文件

```bash
touch /tmp/config.ini
vim config.ini
```

```text
[Camera]  ##相机相关参数
Level = DEBUG                   ## 日志输出等级
FrontRecord = False             ## 录制前相机
BackRecord = False              ## 录制后相机
LeftRecord = False              ## 录制侧相机

[Web] ##网络相关参数
ServiceType = 三宝科技                  ## 服务类型

[Ftp]  ## Ftp相关参数
FtpIpAddress = 192.168.29.156           ## Ftp地址
FtpUserName = ftpsamples                ## FTP用户
FtpPassWd = samples                     ## FTP密码


[Time]  ##时间参数ｚ
NOBOXWAITTIME =   8             ## 没有集装箱结果的超时(空车超时时间)
MAXBOXWAITTIME =   14           ## 箱号识别服务最大超时时间
STARTTIMERED = 2                ## 开始时间向前冗余
ABNORMALSTARTTIMERED = 15       ## 异常结束向前冗余
LASTBOXDURATIONPASSTIME = 2     ## 最后一个集装箱和过卡的时间差
WAITPLATERESULTTIME = 0         ## 返回箱号结果前,带上车牌识别的结果,如果没有最新的车牌结果,最多等待2s,0s表示不接受车牌结果
DETECTFPS = 5                   ## 每隔X帧检测一次,越低抽的图片越多
MAXDURATIONCARFRAMESIZE = 20    ## 两个车次之间的frame差,每间隔20s重新开启检测,一旦检测到第一个停一会,检测第二次
CAMERAREOPENTIME = 30           ## 相机重新打开时间



[SavePath] ##保存路径地址
Mount_Path = /tmp/                         ## 挂载目录
Root_Path = 箱号识别服务V2.4.4日志-1通道      ## 根目录地址
LOG_PATH = Log/                            ## 日志保存路径
CATCH_CONTA_PIC_PATH = ContaPics/          ## 图片抓拍路
CATCH_PLATE_PIC_PATH = PlatePics/          ## 图片抓拍路
DB_PATH = Results/                         ## 结果返回路径



[Other] ## 其他参数
FixedContainerNumber = 0                      ## 固定箱数
MAXRECCOUNT = 8                               ## 最大识别数量
Version = 2.4.5.1                             ## 版本信息

```

### 启动容器



```bash
docker run   \
  --name ascend-infer \
  --network=host \
  --privileged \
  --device=/dev/davinci0 \
  --device=/dev/davinci_manager \
  --device=/dev/hisi_hdc --device=/dev/devmm_svm \
  -v /usr/local/bin/npu-smi:/usr/local/bin/npu-smi \
  -v /home/data/miniD/driver/lib64:/home/data/miniD/driver/lib64 \
  -v /run/board_cfg.ini:/run/board_cfg.ini \
  -v /tmp:/tmp \
  -v /tmp/config.ini://ContainerOCR/config/config.ini \
  --restart always \
  -e WSPort=8002 \
  -d jadehh/ascend-infer:v1.0.2 \
  bash -c 'bash run.sh && tail -f /usr/local/info.log'
```


### 上传镜像


```bash

nohup docker push  jadehh/ascend-infer:v1.0.3    >> info.log 2>&1 &

```