# Opencv

## cuda11.2

```bash
docker build -t   jadehh/opencv:4.5.2-cuda-11.2.2-arch-7.5-build-ubuntu20.04 . 
```
### 打包镜像
CUDA_ARCH_BIN指的是当前显卡的算力7.5
```bash
docker build --build-arg CUDA_ARCH_BIN="7.5" -t   jadehh/opencv:4.5.2-cuda-11.2.2-arch-7.5-build-ubuntu20.04 . 
```
CUDA_ARCH_BIN指的是当前显卡的算力8.6
```bash
docker build --build-arg CUDA_ARCH_BIN="8.6" -t   jadehh/opencv:4.5.2-cuda-11.2.2-arch-8.6-build-ubuntu20.04 . 
```

### 上传镜像

```bash
docker push jadehh/opencv:4.5.2-cuda-11.2.0-build-ubuntu20.04
```
