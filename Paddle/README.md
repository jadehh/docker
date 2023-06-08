
## Paddle打包环境

```bash
cd 开发环境
docker build -t jadehh/container_ocr:pp-develop-1.0.2 . 
```
### 启动容器

```bash
docker run --name container_ocr-pp-develop \
      -v /home/samples/sda2:/home/samples/sda2 \
      -it jadehh/container_ocr:pp-develop-1.0.2
```


```bash
cd 部署环境
docker build -t jadehh/container_ocr:amd64-release-1.0.2 . 
```

### 启动容器

```bash
nvidia-docker run --name container_ocr-amd64-release-1-0-2  \
         -v /home/samples/sda2:/home/samples/sda2 \
      -it jadehh/container_ocr:amd64-release-1.0.2 
```