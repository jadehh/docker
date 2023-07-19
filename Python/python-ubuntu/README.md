# Python3
### Python3.11 镜像打包
```bash
docker build --build-arg PYTHON_VERSION="3.10.11" --build-arg Operation_VERSION="ubuntu:18.04" -t   jadehh/python:3.10.11-ubuntu18.04 .
```


### 启动

```bash
docker run --name python3.10 -v /mnt/h/PycharmProjects/Github/samples/OpencvCapture:/OpencvCapture -it jadehh/python:3.10.11-ubuntu18.04
```