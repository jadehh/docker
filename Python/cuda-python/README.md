# Python3
### Python3.11 镜像打包
```bash
docker build --build-arg PYTHON_VERSION="3.10.11" -t   jadehh/python:3.10-nvidia-cuda10.0 .
```


### 启动

```bash
docker run --name python3.10 -it jadehh/python:3.10-nvidia-cuda10.0
```