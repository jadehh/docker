# Tensorrt

## runtime
```bash
cd runtime
docker build  -t  jadehh/algorithm:v2.1 .
```


## devel

```bash
cd devel
docker build --build-arg PYTHON_VERSION="3.8.16" -t jadehh/tensorrt:cuda-11.6.2-arch8.6-devel-py3.8 .
```