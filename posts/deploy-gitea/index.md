# 在 Ubuntu 虚拟机上搭建 Gitea 服务器


Gitea 是一款极易搭建的自助 Git 服务, 有点像易操作版的 Gitlab.
今天我将尝试使用 Ubuntu 服务器搭建一个 Gitea 服务

### 搭建环境

* Oracle VirtualBox + Ubuntu 20.04

* 网络连接方式设置为桥接网卡, 高级 -> 混杂模式 -> 全部允许

* 查看 ip : `ifconfig` (先安装 net-tools)

* 使用 PuTTY 测试宿主机是否可以连接虚拟服务器

### 新建 git 账号

```bash
sudo adduser git
sudo adduser git sudo
```

### 创建 PostgreSQL 数据库

```bash
sudo apt-get install postgresql
sudo -u postgres psql
```

```plsql
postgres=# create user gitea with password 'password';
postgres=# create database gitea owner gitea;
```

### 安装 Gitea

下载

```bash
wget -O gitea https://dl.gitea.io/gitea/master/gitea-master-linux-amd64
chmod +x gitea
```

启动服务器

```bash
./gitea web
```

访问 [localhost:3000](http://localhost:3000/) 会看如下页面, 注册账号并设置配置信息

{{< figure src="/images/gitea.png" >}}

### 配置

静态文件根目录: `/home/git`

### 开机启动

编辑 `/etc/systemd/system/gitea.service` 添加以下内容

```ini
[Unit]
Description=Gitea (Git with a cup of tea)
After=syslog.target
After=network.target
#After=mysqld.service
After=postgresql.service
#After=memcached.service
#After=redis.service

[Service]
# Modify these two values and uncomment them if you have
# repos with lots of files and get an HTTP error 500 because
# of that
###
#LimitMEMLOCK=infinity
#LimitNOFILE=65535
RestartSec=2s
Type=simple
User=git
Group=git
WorkingDirectory=/home/git/
ExecStart=/home/git/gitea web --config /home/git/custom/conf/app.ini
Restart=always
Environment=USER=git HOME=/home/git

[Install]
WantedBy=multi-user.target
```

重启

```bash
sudo systemctl daemon-reload
sudo systemctl start gitea
```

开机启动

```bash
sudo systemctl enable gitea.service
```

完成搭建过程, 可以看到 Gitea 的搭建就是这么简单方便, 有兴趣的可以自己尝试看看.
