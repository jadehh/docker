# Miniconda3
## aarch64
### 打包镜像
```bash
cd aarch64
docker build -t jadehh/miniconda3:aarch64-4.9.2 . 
```

## 上传镜像

```bash
docker push jadehh/miniconda3:aarch64-4.9.2 
```

## amd64
### 打包镜像

```bash
cd amd64
docker build -t jadehh/miniconda3:amd64-4.9.2 . 
```

## 上传镜像

```bash
docker push jadehh/miniconda3:amd64-4.9.2 
```