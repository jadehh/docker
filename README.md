# ONNX

## devel
```bash
cd 开发环境
docker build --build-arg CUDA_ARCH_BIN="7.5"  --build-arg Operation_VERSION="ubuntu18.04"  --build-arg CUDA_VERSION="10.0"  -t  jadehh/onnx:11.6.2-arch-7.5-devel-ubuntu18.04  .
docker build --build-arg CUDA_ARCH_BIN="8.6"  --build-arg Operation_VERSION="ubuntu18.04"  --build-arg CUDA_VERSION="11.6.2"  -t  jadehh/onnx:11.6.2-arch-8.6-devel-ubuntu18.04  .
```
## runtime
```bash
cd 开发环境
docker build --build-arg CUDA_ARCH_BIN="8.6"  --build-arg Operation_VERSION="ubuntu18.04"  --build-arg CUDA_VERSION="11.6.2"    -t  jadehh/video_stitching:onnx-11.6.2-arch-7.5-devel-ubuntu18.04  .
```

