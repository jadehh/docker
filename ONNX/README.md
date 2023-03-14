## Docker部署环境

### 打包镜像
```bash
cd 部署环境
docker build -t jadehh/container_ocr:onnx-release-1.0.1 .  
```
#### 启动容器

```bash
docker run --privileged  \
           --network=host   \
           --name container-ocr-onnx-release \
           -v /home/samples/sda2:/home/samples/sda2 \
           -v /home/samples/Data:/home/samples/Data \
          -it jadehh/container_ocr:onnx-release-1.0.1 
```

### 上传Docker镜像

```bash
docker push jadehh/container_ocr:onnx-release-1.0.1
```
