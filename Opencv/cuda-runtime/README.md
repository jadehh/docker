# Opencv-Cuda

### cuda-runtime镜像打包
CUDA_ARCH_BIN指的是当前显卡的算力7.5
```bash
docker build  --build-arg PYTHON_VERSION="3.10.11" --build-arg CUDA_ARCH_BIN="7.5"  --build-arg CUDA_VERSION="10.0"    --build-arg CUDNN_VERSION="7"  -t  jadehh/opencv-cuda:10.0-arch7.5-runtime-py3.10 .
```
CUDA_ARCH_BIN指的是当前显卡的算力8.6
```bash
docker build --build-arg PYTHON_VERSION="3.10.11" --build-arg CUDA_ARCH_BIN="8.6"   --build-arg CUDA_VERSION="11.6.2"  --build-arg CUDNN_VERSION="8"  -t  jadehh/opencv-cuda:11.6.2-arch8.6-runtime-py3.10 .
```

### 启动
wsl 启动
```bash
docker run --name opencv-cuda-runtime --gpus=all -v /mnt/c/Windows/System32/lxss/lib/libnvcuvid.so.1:/usr/lib/x86_64-linux-gnu/libnvcuvid.so.1 -v /mnt/c/Windows/System32/lxss/lib/libnvidia-encode.so.1:/usr/lib/x86_64-linux-gnu/libnvidia-encode.so.1 -d  jadehh/opencv-cuda:10.0-arch7.5-runtime-py3.10  bash -c " ./OpencvCapture -camera_ip=192.168.29.181 -camera_username=admin -camera_passwd=samples123 --use_gpu=True"
```


普通Ubuntu启动

```bash
docker run --name  opencv-cuda-runtime  -v /usr/lib/x86_64-linux-gnu/libnvcuvid.so.1:/usr/lib/x86_64-linux-gnu/libnvcuvid.so.1 -v  /usr/lib/x86_64-linux-gnu/libnvidia-encode.so.1:/usr/lib/x86_64-linux-gnu/libnvidia-encode.so.1 -d jadehh/opencv-cuda:11.6.2-arch8.6-runtime-py3.10  bash -c " ./OpencvCapture -camera_ip=192.168.29.181 -camera_username=admin -camera_passwd=samples123 --use_gpu=True "
```
