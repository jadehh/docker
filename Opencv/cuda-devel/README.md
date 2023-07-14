# Opencv-Cuda

### cuda-devel镜像打包
CUDA_ARCH_BIN指的是当前显卡的算力7.5
Ubuntu18.04对应的是python3.6 Ubuntu20.04对应的是python3.10
CUDA版本分为10.0和11.6.2两个版本
```bash
docker build --build-arg CUDA_ARCH_BIN="7.5" --build-arg Operation_VERSION="ubuntu18.04"   --build-arg CPU_THERAD_COMPILE="16"  --build-arg CUDA_VERSION="10.0"    --build-arg CUDNN_VERSION="7"  -t   jadehh/opencv-cuda:10.0-arch-7.5-opencv4-8-0-devel-ubuntu18.04 .
docker build --build-arg CUDA_ARCH_BIN="7.5" --build-arg Operation_VERSION="ubuntu18.04"   --build-arg CPU_THERAD_COMPILE="16"  --build-arg CUDA_VERSION="11.6.2"  --build-arg CUDNN_VERSION="8"  -t   jadehh/opencv-cuda:11.6.2-arch-7.5-opencv4-8-0-devel-ubuntu18.04 .
docker build --build-arg CUDA_ARCH_BIN="7.5" --build-arg Operation_VERSION="ubuntu20.04"   --build-arg CPU_THERAD_COMPILE="16"  --build-arg CUDA_VERSION="11.6.2"  --build-arg CUDNN_VERSION="8"  -t   jadehh/opencv-cuda:11.6.2-arch-7.5-opencv4-8-0-devel-ubuntu22.04 .
```
> cuda环境不同需要升级显卡驱动
> 操作系统不同对应的python环境也不同
> 20.04升级成22.04,使用22.04源

CUDA_ARCH_BIN指的是当前显卡的算力8.6

```bash
docker build --build-arg CUDA_ARCH_BIN="8.6"  --build-arg CPU_THERAD_COMPILE="32" --build-arg Operation_VERSION="ubuntu18.04"  --build-arg CUDA_VERSION="11.6.2"  --build-arg CUDNN_VERSION="8"  -t   jadehh/opencv-cuda:11.6.2-arch-8.6-opencv4-8-0-devel-ubuntu18.04 .
docker build --build-arg CUDA_ARCH_BIN="8.6"  --build-arg CPU_THERAD_COMPILE="32" --build-arg Operation_VERSION="ubuntu20.04"  --build-arg CUDA_VERSION="11.6.2"  --build-arg CUDNN_VERSION="8"  -t   jadehh/opencv-cuda:11.6.2-arch-8.6-opencv4-8-0-devel-ubuntu22.04 .
```
> 算力为8.6不支持CUDA10


### 测试视频流解码
需要使用本机的libnvicuvid.so和libnvidia-encode.so.1
```bash
cv2.cudacodec.createVideoReader("rtsp://admin:samples123@192.168.29.182:554/h264/ch1/main/av_stream")
```
### 启动
wsl 启动
```bash
docker run --name opencv-cuda --gpus=all -v /mnt/c/Windows/System32/lxss/lib/libnvcuvid.so.1:/usr/lib/x86_64-linux-gnu/libnvcuvid.so.1 -v /mnt/c/Windows/System32/lxss/lib/libnvidia-encode.so.1:/usr/lib/x86_64-linux-gnu/libnvidia-encode.so.1 -d jadehh/opencv-cuda:10.0-arch-7.5-opencv4-8-0-devel-ubuntu18.04  bash -c " ./OpencvCapture -camera_ip=192.168.29.181 -camera_username=admin -camera_passwd=samples123 --use_gpu=True"
docker run --name opencv-cuda --gpus=all -v /mnt/c/Windows/System32/lxss/lib/libnvcuvid.so.1:/usr/lib/x86_64-linux-gnu/libnvcuvid.so.1 -v /mnt/c/Windows/System32/lxss/lib/libnvidia-encode.so.1:/usr/lib/x86_64-linux-gnu/libnvidia-encode.so.1 -d jadehh/opencv-cuda:11.6.2-arch-7.5-opencv4-8-0-devel-ubuntu18.04  bash -c " ./OpencvCapture -camera_ip=192.168.29.181 -camera_username=admin -camera_passwd=samples123 --use_gpu=True"

docker run --name opencv-cuda --gpus=all -v /mnt/c/Windows/System32/lxss/lib/libnvcuvid.so.1:/usr/lib/x86_64-linux-gnu/libnvcuvid.so.1 -v /mnt/c/Windows/System32/lxss/lib/libnvidia-encode.so.1:/usr/lib/x86_64-linux-gnu/libnvidia-encode.so.1 -d jadehh/opencv-cuda:11.6.2-arch-7.5-opencv4-8-0-devel-ubuntu22.04  bash -c " ./OpencvCapture -camera_ip=192.168.29.181 -camera_username=admin -camera_passwd=samples123 --use_gpu=True"

```
拷贝opencv环境
```bash
docker cp opencv-cuda:/opencv-cuda-10.0-cudnn7-arch-7.5-ubuntu18.04.tar.gz ./
docker cp opencv-cuda:/opencv-cuda-10.0-cudnn7-arch-7.5-ubuntu18.04.tar.gz ./

```

普通Ubuntu启动

```bash
docker run --name  opencv-cuda  -v /usr/lib/x86_64-linux-gnu/libnvcuvid.so.1:/usr/lib/x86_64-linux-gnu/libnvcuvid.so.1 -v  /usr/lib/x86_64-linux-gnu/libnvidia-encode.so.1:/usr/lib/x86_64-linux-gnu/libnvidia-encode.so.1 -d jadehh/opencv-cuda:11.6.2-arch-8.6-opencv4-8-0-devel-ubuntu18.04  bash -c " ./OpencvCapture -camera_ip=192.168.29.181 -camera_username=admin -camera_passwd=samples123 --use_gpu=True "
```
拷贝opencv环境
```bash
docker cp opencv-cuda:/opencv-cuda-11.6.2-cudnn8-arch-8.6-ubuntu18.04.tar.gz ./
```