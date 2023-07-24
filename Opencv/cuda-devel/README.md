# Opencv-Cuda

### cuda-devel镜像打包
CUDA_ARCH_BIN指的是当前显卡的算力7.5
Python版本python3.10
CUDA版本分为10.0和11.6.2两个版本
```bash
docker build --build-arg PYTHON_VERSION="3.8.16"  --build-arg CUDA_ARCH_BIN="7.5"    --build-arg CUDA_VERSION="10.2"    --build-arg CUDNN_VERSION="8"  -t   jadehh/opencv-cuda:10.2-arch7.5-devel-py3.8 .

```
> 为了兼容高版本和低版本选择CUDA10.2,并使用Python3.8.16版本,低版本的ONNX不支持Python3.10


> cuda环境不同需要升级显卡驱动
> 操作系统不同对应的python环境也不同

CUDA_ARCH_BIN指的是当前显卡的算力8.6

```bash
docker build --build-arg PYTHON_VERSION="3.10.11" --build-arg CUDA_ARCH_BIN="8.6"   --build-arg CUDA_VERSION="11.6.2"  --build-arg CUDNN_VERSION="8"  -t   jadehh/opencv-cuda:11.6.2-arch8.6-devel-py3.10 .
docker build --build-arg PYTHON_VERSION="3.8.16"  --build-arg CUDA_ARCH_BIN="8.6"   --build-arg CUDA_VERSION="11.6.2"  --build-arg CUDNN_VERSION="8"  -t   jadehh/opencv-cuda:11.6.2-arch8.6-devel-py3.8 .

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

docker run --name opencv-cuda --gpus=all -v /mnt/c/Windows/System32/lxss/lib/libnvcuvid.so.1:/usr/lib/x86_64-linux-gnu/libnvcuvid.so.1 -v /mnt/c/Windows/System32/lxss/lib/libnvidia-encode.so.1:/usr/lib/x86_64-linux-gnu/libnvidia-encode.so.1 -d jadehh/opencv-cuda:10.0-arch7.5-devel-py3.10  bash -c " ./OpencvCapture -camera_ip=192.168.29.181 -camera_username=admin -camera_passwd=samples123 --use_gpu=True"
docker run --name opencv-cuda --gpus=all -v /mnt/c/Windows/System32/lxss/lib/libnvcuvid.so.1:/usr/lib/x86_64-linux-gnu/libnvcuvid.so.1 -v /mnt/c/Windows/System32/lxss/lib/libnvidia-encode.so.1:/usr/lib/x86_64-linux-gnu/libnvidia-encode.so.1 -d jadehh/opencv-cuda:10.2-arch7.5-devel-py3.8   bash -c " ./OpencvCapture -camera_ip=192.168.29.181 -camera_username=admin -camera_passwd=samples123 --use_gpu=True"
docker run --name opencv-cuda --gpus=all -v /mnt/c/Windows/System32/lxss/lib/libnvcuvid.so.1:/usr/lib/x86_64-linux-gnu/libnvcuvid.so.1 -v /mnt/c/Windows/System32/lxss/lib/libnvidia-encode.so.1:/usr/lib/x86_64-linux-gnu/libnvidia-encode.so.1 -v /mnt/h/PycharmProjects/Github/ContainerOCR:/ContainerOCR -d jadehh/opencv-cuda:10.2-arch7.5-devel-py3.8   bash -c " ./OpencvCapture -camera_ip=192.168.29.181 -camera_username=admin -camera_passwd=samples123 --use_gpu=True"

```
拷贝opencv环境
```bash
docker cp opencv-cuda:/opencv-cuda-10.2-cudnn8-arch-7.5-py3.8.gz ./
```

普通Ubuntu启动

```bash
docker run --name  opencv-cuda -v /home/samples/sda2:/home/samples/sda2 -v /usr/lib/x86_64-linux-gnu/libnvcuvid.so.1:/usr/lib/x86_64-linux-gnu/libnvcuvid.so.1 -v  /usr/lib/x86_64-linux-gnu/libnvidia-encode.so.1:/usr/lib/x86_64-linux-gnu/libnvidia-encode.so.1 -it jadehh/opencv-cuda:11.6.2-arch8.6-devel-py3.8 

docker run --name  opencv-cuda  -v /usr/lib/x86_64-linux-gnu/libnvcuvid.so.1:/usr/lib/x86_64-linux-gnu/libnvcuvid.so.1 -v  /usr/lib/x86_64-linux-gnu/libnvidia-encode.so.1:/usr/lib/x86_64-linux-gnu/libnvidia-encode.so.1 -d jadehh/opencv-cuda:11.6.2-arch8.6-devel-py3.10  bash -c " ./OpencvCapture -camera_ip=192.168.29.181 -camera_username=admin -camera_passwd=samples123 --use_gpu=True "
docker run --name  opencv-cuda  -v /usr/lib/x86_64-linux-gnu/libnvcuvid.so.1:/usr/lib/x86_64-linux-gnu/libnvcuvid.so.1 -v  /usr/lib/x86_64-linux-gnu/libnvidia-encode.so.1:/usr/lib/x86_64-linux-gnu/libnvidia-encode.so.1 -d jadehh/opencv-cuda:11.6.2-arch8.6-devel-py3.8   bash -c " ./OpencvCapture -camera_ip=192.168.29.181 -camera_username=admin -camera_passwd=samples123 --use_gpu=True "

```
拷贝opencv环境
```bash
docker cp opencv-cuda:/opencv-cuda-11.6.2-cudnn8-arch-8.6-py3.10.gz ./
docker cp opencv-cuda:/opencv-cuda-11.6.2-cudnn8-arch-8.6-py3.8.gz ./
```