---
lang: 'zh-CN'
title: 'Docker参考'
description: '这个项目将会记录学习过程中的知识点！'
---
## 离线安装 Docker
### 准备
- [docker-20.10.23.tgz](https://download.docker.com/linux/static/stable/x86_64/docker-20.10.23.tgz)
- docker.service 文件
```md
[Unit]
Description=Docker Application Container Engine
Documentation=https://docs.docker.com
After=network-online.target firewalld.service
Wants=network-online.target
[Service]
Type=notify
# the default is not to use systemd for cgroups because the delegate issues still
# exists and systemd currently does not support the cgroup feature set required
# for containers run by docker
ExecStart=/usr/bin/dockerd
ExecReload=/bin/kill -s HUP $MAINPID
# Having non-zero Limit*s causes performance problems due to accounting overhead
# in the kernel. We recommend using cgroups to do container-local accounting.
LimitNOFILE=infinity
LimitNPROC=infinity
LimitCORE=infinity
# Uncomment TasksMax if your systemd version supports it.
# Only systemd 226 and above support this version.
#TasksMax=infinity
TimeoutStartSec=0
# set delegate yes so that systemd does not reset the cgroups of docker containers
Delegate=yes
# kill only the docker process, not all processes in the cgroup
KillMode=process
# restart the docker process if it exits prematurely
Restart=on-failure
StartLimitBurst=3
StartLimitInterval=60s
 
[Install]
WantedBy=multi-user.target
```

### 安装
```bash
# 解压 docker tar 包
tar -xvf docker-20.10.23.tgz
# 将 docker 目录移到 /usr/bin 目录下
cp docker/* /usr/bin/
# 将docker.service 移到/etc/systemd/system/ 目录
cp docker.service /etc/systemd/system/
# 添加文件权限
chmod +x /etc/systemd/system/docker.service
# 重新加载配置文件
systemctl daemon-reload
# 启动 docker
systemctl start docker
# 设置开机启动
systemctl enable docker.service
# 验证
docker -v
```

### 卸载
```bash
# 停止 docker 
systemctl stop docker
# 删除开机启动
systemctl disable docker
# 删除docker.service
rm -f /etc/systemd/system/docker.service
# 删除docker文件
rm -rf /usr/bin/docker* /usr/bin/containerd* /usr/bin/runc /usr/bin/ctr
# 重新加载配置文件
systemctl daemon-reload
```

## 离线安装 Docker Compose
### 准备
- [docker-compose-linux-x86_64](https://gh.api.99988866.xyz/https://github.com/docker/compose/releases/download/v2.16.0/docker-compose-linux-x86_64)

### 安装
```bash
# 将下载好的 docker-compose 重命名并移到 /usr/local/bin 目录下
mv docker-compose-linux-x86_64 /usr/local/bin/docker-compose
# 添加文件权限
chmod +x /usr/local/bin/docker-compose
# 验证
docker-compose -v
```

## 镜像操作
### save
语法
```bash
docker save [OPTIONS] IMAGE [IMAGE...]
```
OPTIONS 说明：
- -o :输出到的文件。

示例如下：
```bash
docker save -o mysql.8.0.30.tar.gz mysql:8.0.30
```

### load
语法
```bash
docker load [OPTIONS]
```
OPTIONS 说明：
- --input , -i : 指定导入的文件，代替 STDIN。

- --quiet , -q : 精简输出信息

示例如下：
```bash
docker load < mysql.8.0.30.tar.gz
```