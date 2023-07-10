# Opencv-Cuda

### ubuntu18.04 cuda11.6 部署镜像
CUDA_ARCH_BIN指的是当前显卡的算力7.5
```bash
docker build  --build-arg CUDA_ARCH_BIN="7.5"  --build-arg Operation_VERSION="ubuntu18.04"   --build-arg Operation_VERSION="ubuntu18.04"  --build-arg CUDA_VERSION="11.6.2"  --build-arg CUDNN_VERSION="8"  -t   jadehh/opencv-cuda:11.6.2-arch-7.5-opencv4-8-0-runtime-ubuntu18.04 .
```
CUDA_ARCH_BIN指的是当前显卡的算力8.6

```bash
docker build  --build-arg CUDA_ARCH_BIN="8.6"  --build-arg Operation_VERSION="ubuntu18.04"   --build-arg Operation_VERSION="ubuntu18.04"  --build-arg CUDA_VERSION="11.6.2"  --build-arg CUDNN_VERSION="8"  -t   jadehh/opencv-cuda:11.6.2-arch-8.6-opencv4-8-0-runtime-ubuntu18.04 .
```

### 启动
wsl 启动
```bash
docker run --name opencv-cuda-runtime --gpus=all -v /mnt/c/Windows/System32/lxss/lib/libnvcuvid.so.1:/usr/lib/x86_64-linux-gnu/libnvcuvid.so.1 -v /mnt/c/Windows/System32/lxss/lib/libnvidia-encode.so.1:/usr/lib/x86_64-linux-gnu/libnvidia-encode.so.1 -d jadehh/opencv-cuda:11.6.2-arch-7.5-opencv4-8-0-runtime-ubuntu18.04  bash -c " ./OpencvCapture -camera_ip=192.168.29.181 -camera_username=admin -camera_passwd=samples123 --use_gpu=True "
```

ubuntu 启动
```bash
docker run --name  opencv-cuda-runtime  -v /usr/lib/x86_64-linux-gnu/libnvcuvid.so.1:/usr/lib/x86_64-linux-gnu/libnvcuvid.so.1 -v  /usr/lib/x86_64-linux-gnu/libnvidia-encode.so.1:/usr/lib/x86_64-linux-gnu/libnvidia-encode.so.1 -d jadehh/opencv-cuda:11.6.2-arch-8.6-opencv4-8-0-runtime-ubuntu18.04  bash -c " ./OpencvCapture -camera_ip=192.168.29.181 -camera_username=admin -camera_passwd=samples123 --use_gpu=True "

```