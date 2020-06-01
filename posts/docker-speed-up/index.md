# Docker 镜像加速


1. 使用阿里云镜像加速器, [网址](https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors)

2. 复制加速器地址

3. 修改 Docker 的镜像 URL

```json
"registry-mirrors": [
    "https://registry.docker-cn.com"  # 改为加速器的地址
  ]
```

