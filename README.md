# ONNX


## runtime
```bash
cd 开发环境
docker build --build-arg PYTHON_VERSION="3.10" --build-arg CUDA_ARCH_BIN="7.5" --build-arg CUDA_VERSION="10.0"   -t  jadehh/algorithm:onnx-arch-7.5-runtime-py3.10 .
docker build --build-arg PYTHON_VERSION="3.10" --build-arg CUDA_ARCH_BIN="8.6" --build-arg CUDA_VERSION="11.6.2" -t  jadehh/algorithm:onnx-arch-8.6-runtime-py3.10 .

```

