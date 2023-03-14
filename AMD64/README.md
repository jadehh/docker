## Amd64

## Amd64打包环境

```bash
cd 打包环境
docker build -t jadehh/container_ocr:amd64-packing-1.0.1 .
```

### 启动容器

```bash
docker run --name container_ocr-ascend-packing \
           -v /root/jade:/root/jade \
          -it jadehh/container_ocr:amd64-packing-1.0.1
```
