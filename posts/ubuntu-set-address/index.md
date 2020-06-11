# Ubuntu 系统设置 IP 地址


Ubuntu 面前支持新的网络配置工具 Netplan, 可通过配置 `etc/netplan/` 目录下的 `yaml` 文件设置主机的 IP 地址

#### 进入 netplan 目录

`cd /etc/netplan`

#### 配置 yaml 文件

不一定是这个文件名, 先通过 `ls` 命令看一下

```bash
ls
sudo vim 00-installer-config.yaml
```

请参考如下内容

```yaml
# This is the network config written by 'subiquity'
network:
  ethernets:
    enp0s3:
      dhcp4: true
      addresses : [192.168.2.118/24]
  version: 2
```

#### 使配置生效

`netplan apply`

