# Docker

## SSH

### Docker镜像制作

```bash
cd ssh
docker build -t jadehh/ubuntu:ssh-qt-24.04 .
```

### 启动镜像


```bash
nvidia-docker run   \
  --name ubuntu \
  --net host \
  -itd \
  --privileged \
  -v /tmp/.X11-unix:/tmp/.X11-unix \
  -e DISPLAY=$DISPLAY \
  --restart=always \
   jadehh/ubuntu:ssh-qt-24.04 /sbin/init
```
