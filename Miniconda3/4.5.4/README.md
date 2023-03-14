# Miniconda3
## amd64
### 打包镜像

```bash
cd amd64
docker build -t jadehh/miniconda3:amd64-4.5.4 . 
```

## 上传镜像

```bash
docker push jadehh/miniconda3:amd64-4.5.4
```