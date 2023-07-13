# VideoStitching

## 打包镜像
```bash
cd 部署环境
docker build -t jadehh/video_stitching:amd64-release-1.0.1 .  
```
## 开发环境
```bash
cd 开发环境
docker build --build-arg CUDA_ARCH_BIN="8.6"  --build-arg Operation_VERSION="ubuntu18.04"  --build-arg CUDA_VERSION="11.6.2"    -t  jadehh/video_stitching:onnx-11.6.2-arch-7.5-devel-ubuntu18.04  .
```

启动容器

```bash
docker run --name  video-stitching-devel   -v /usr/lib/x86_64-linux-gnu/libnvcuvid.so.1:/usr/lib/x86_64-linux-gnu/libnvcuvid.so.1 -v  /usr/lib/x86_64-linux-gnu/libnvidia-encode.so.1:/usr/lib/x86_64-linux-gnu/libnvidia-encode.so.1 -v /home/samples/sda2:/home/samples/sda2 -it jadehh/video_stitching:onnx-11.6.2-arch-7.5-devel-ubuntu18.04 
```