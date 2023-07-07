# Opencv-Cuda

### ubuntu18.04 cuda11.6 打包镜像
CUDA_ARCH_BIN指的是当前显卡的算力7.5
```bash
docker build --build-arg CUDA_ARCH_BIN="7.5"  --build-arg CPU_THERAD_COMPILE="16" --build-arg Operation_VERSION="ubuntu18.04"  --build-arg CUDA_VERSION="11.6.2"  --build-arg CUDNN_VERSION="8"  -t   jadehh/opencv-cuda:11.6.2-arch-7.5-opencv4-8-0-build-ubuntu18.04 . 
```
CUDA_ARCH_BIN指的是当前显卡的算力8.6
```bash
docker build --build-arg CUDA_ARCH_BIN="8.6"  --build-arg CPU_THERAD_COMPILE="32" --build-arg Operation_VERSION="ubuntu18.04"  --build-arg CUDA_VERSION="11.6.2"  --build-arg CUDNN_VERSION="8"  -t   jadehh/opencv-cuda:11.6.2-arch-8.6-opencv4-8-0-build-ubuntu18.04 . 
```

### 上传镜像

```bash
docker push jadehh/opencv:4.5.2-cuda-11.2.0-build-ubuntu20.04
```


### 测试视频流解码
需要使用本机的libnvicuvid.so和libnvidia-encode.so.1
```bash
cv2.cudacodec.createVideoReader("rtsp://admin:samples123@192.168.29.182:554/h264/ch1/main/av_stream")
```