# Docker 镜像加速


* 使用阿里云镜像加速器, [网址](https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors)

* 复制加速器地址

* Ubuntu 系统通过修改daemon配置文件`/etc/docker/daemon.json`来使用加速器

```bash
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://****.mirror.aliyuncs.com"]  # 改成自己加速地址
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

