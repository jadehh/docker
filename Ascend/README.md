## Ascend开发环境

### 构建Image

```bash
cd 开发环境
docker build -t jadehh/container_ocr:ascend-develop-1.0.3 .
```

### 启动容器

```bash
docker run   \
  --name container-ocr \
  --network=host \
  --privileged \
  --device=/dev/davinci0 \
  --device=/dev/davinci_manager \
  --device=/dev/hisi_hdc --device=/dev/devmm_svm \
  -v /usr/local/bin/npu-smi:/usr/local/bin/npu-smi \
  -v /home/data/miniD/driver/lib64:/home/data/miniD/driver/lib64 \
  -v /run/board_cfg.ini:/run/board_cfg.ini \
  -v /tmp:/tmp \
  -it jadehh/container_ocr:ascend-develop-1.0.3
  
docker run   \
  --name container-capture \
  --network=host \
  --privileged \
  --device=/dev/davinci0 \
  --device=/dev/davinci_manager \
  --device=/dev/hisi_hdc --device=/dev/devmm_svm \
  -v /usr/local/bin/npu-smi:/usr/local/bin/npu-smi \
  -v /home/data/miniD/driver/lib64:/home/data/miniD/driver/lib64 \
  -v /run/board_cfg.ini:/run/board_cfg.ini \
  -v /tmp:/tmp \
  -it jadehh/container_ocr:ascend-develop-1.0.3
  
 docker run   \
  --name container-tools \
  --network=host \
  --privileged \
  --device=/dev/davinci0 \
  --device=/dev/davinci_manager \
  --device=/dev/hisi_hdc --device=/dev/devmm_svm \
  -v /usr/local/bin/npu-smi:/usr/local/bin/npu-smi \
  -v /home/data/miniD/driver/lib64:/home/data/miniD/driver/lib64 \
  -v /run/board_cfg.ini:/run/board_cfg.ini \
  -v /tmp:/tmp \
  -it jadehh/container_ocr:ascend-develop-1.0.3
```


## Ascend打包环境

```bash
cd 打包环境
docker build -t jadehh/container_ocr:ascend-packing-1.0.3 .
```

### 启动容器

```bash
docker run --name container_ocr-ascend-packing \
           -v /root/jade:/root/jade \
          -it jadehh/container_ocr:ascend-packing-1.0.3 
```

## Ascend部署环境

### 构建Image

```bash
docker build -t jadehh/container_ocr:ascend-release-1.0.3 .
```
### 启动容器

```bash
docker run   \
  --name ubuntu \
  -itd \
  --network=host \
  --privileged \
  --device=/dev/davinci0 \
  --device=/dev/davinci_manager \
  --device=/dev/hisi_hdc --device=/dev/devmm_svm \
  -v /usr/local/bin/npu-smi:/usr/local/bin/npu-smi \
  -v /var/hasplm:/var/hasplm -v /etc/hasplm:/etc/hasplm \
  -v /home/data/miniD/driver/lib64:/home/data/miniD/driver/lib64 \
  -v /run/board_cfg.ini:/run/board_cfg.ini \
  -v /home/samples/sda2:/home/samples/sda2 \
  --restart=always \
   jadehh/container_ocr:ascend-release-1.0.3 /sbin/init

```

### 上传镜像

```bash
docker push  jadehh/container_ocr:ascend-release-1.0.1

```

