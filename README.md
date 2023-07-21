# ONNX


## runtime
```bash
cd 开发环境
docker build --build-arg PYTHON_VERSION="3.8" --build-arg CUDA_ARCH_BIN="7.5" --build-arg CUDA_VERSION="10.2"   -t  jadehh/algorithm:onnx-arch-7.5-runtime-py3.8 .
docker build --build-arg PYTHON_VERSION="3.8" --build-arg CUDA_ARCH_BIN="8.6" --build-arg CUDA_VERSION="11.6.2" -t  jadehh/algorithm:onnx-arch-8.6-runtime-py3.8 .

```

