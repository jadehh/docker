# Miniconda3

## 打包镜像

```bash
docker build -t jadehh/miniconda3-aarch64:v1.0.1 . 
```

## 启动容器

```bash
docker run --name miniconda3 -v /tmp:/tmp -v /root/jade:/root/jade -it  jadehh/miniconda3-aarch64:v1.0.1 
```

## 上传镜像

```bash
docker push jadehh/miniconda3-aarch64:v1.0.1 
```