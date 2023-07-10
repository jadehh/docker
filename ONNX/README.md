## Docker部署环境


### 开发环境

```bash

cd 开发环境
docker build --build-arg CUDA_ARCH_BIN="7.5"  --build-arg Operation_VERSION="ubuntu18.04"  --build-arg CUDA_VERSION="11.6.2"    -t  jadehh/container_ocr:onnx-11.6.2-arch-7.5-devel-ubuntu18.04  .

```

### 启动容器
```bash
docker run --name onnx-devel --gpus=all -v /mnt/c/Windows/System32/lxss/lib/libnvcuvid.so.1:/usr/lib/x86_64-linux-gnu/libnvcuvid.so.1 -v /mnt/c/Windows/System32/lxss/lib/libnvidia-encode.so.1:/usr/lib/x86_64-linux-gnu/libnvidia-encode.so.1 -v /mnt/h/PycharmProjects/Github/ContainerOCR:/ContainerOCR -it jadehh/container_ocr:onnx-11.6.2-arch-7.5-devel-ubuntu18.04 

```


### 打包镜像
```bash
cd 部署环境
docker build --build-arg CUDA_ARCH_BIN="7.5"  --build-arg Operation_VERSION="ubuntu18.04"  --build-arg CUDA_VERSION="11.6.2"    -t  jadehh/container_ocr:onnx-11.6.2-arch-7.5-runtime-ubuntu18.04  .

```
#### 启动容器

```bash
docker run --name onnx-runtime --gpus=all -v /mnt/c/Windows/System32/lxss/lib/libnvcuvid.so.1:/usr/lib/x86_64-linux-gnu/libnvcuvid.so.1 -v /mnt/c/Windows/System32/lxss/lib/libnvidia-encode.so.1:/usr/lib/x86_64-linux-gnu/libnvidia-encode.so.1 -v /mnt/h/PycharmProjects/Github/ContainerOCR:/ContainerOCR -it jadehh/container_ocr:onnx-11.6.2-arch-7.5-runtime-ubuntu18.04 

```

### 上传Docker镜像

```bash
docker push jadehh/container_ocr:onnx-release-1.0.1
```
