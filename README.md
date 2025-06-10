# ONNX


## runtime
```bash
cd runtime/cuda11
docker build  -t  jadehh/algorithm:v1.2 .
```

```bash
cd runtime/cuda10
docker build  -t  jadehh/algorithm:v1.1 .
```
> 适用于显卡驱动为440的版本，注意如果Onnx opset版本为11以上，请升级显卡驱动