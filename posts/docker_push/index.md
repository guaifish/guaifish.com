# 提交镜像到 Docker Hub


#### 注册账号

首先需要到官网 [Docker Hub](https://hub.docker.com/) 注册一个账号

#### 本地登录

运行下面命令, 输入自己的账号密码

`docker login`

#### 打标签

给 docker 镜像打标签, 改为自己的用户名

`docker tag todoapp guaifish/todoapp`

#### 提交

`docker push`

