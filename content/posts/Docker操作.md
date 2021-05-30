---
title: 'Docker基本设置'
date: 2020-04-10 06:17:09
toc: true
authors: [graundcian]
tags: [Docker]
---


设置镜像加速和代理
<!--more-->

# 设置

## 镜像加速

```bash
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://md5153cu.mirror.aliyuncs.com"]
}
EOF

sudo systemctl daemon-reload
sudo systemctl restart docker
```

## 代理

```bash
sudo mkdir -p /etc/systemd/system/docker.service.d
sudo tee /etc/systemd/system/docker.service.d/http-proxy.conf <<-'EOF'
[Service]
Environment="HTTP_PROXY=http://192.168.0.120:7890/"
Environment="HTTPS_PROXY=https://192.168.0.120:7890/
EOF

sudo systemctl daemon-reload
sudo systemctl restart docker
```