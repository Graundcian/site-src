---
title: 'Raspberry-Pi4安装Resilio-Sync'
date: 2020-03-13 17:47:08
tags: [Raspberry-Pi]
---



💡Resilio Syn（BitTorrent Sync）是由BitTorrent公司开发的专有的对等网络数据同步工具，其可在局域网、互联网上通过安全的、分布式的P2P技术在不同设备之间同步文件。

<!-- more -->

仅记录以 **deb** 包的方式安装，另外可以包管理工具进行安装，但较为繁琐。参见[Sync官方文档](https://help.resilio.com/hc/en-us/articles/206178924)

### 下载

Resilio Sync官网下载arm64架构[deb软件包。](https://download-cdn.resilio.com/2.6.4.1344/Debian/resilio-sync_2.6.4.1344-1_arm64.deb)

### 安装

```bash
sudo dpkg -i <resilio-sync.deb>
```

### 试用 Pro 版

修改系统时间为未来，例如：

```bash
sudo date -s 13/03/2023
```
然后在管理界面点击试用 Pro 版，再将系统时间改回当前时间。

### 管理

使用 **System**进行管理，在 **rslsync** 用户下开启开机自启动。

```bash
sudo systemctl enable resilio-sync
```

出于安全原因，默认情况下使用具有最低权限的 **rslsync** 用户。因此，如果需要同步当前用户拥有的文件，只需将**rslsync** 用户添加到当前用户的组中，并确保要同步的文件夹对所述组具有读写权限，例如：

```bash
sudo usermod -aG user_group rslsync
sudo usermod -aG rslsync user_name
sudo chmod g+rw synced_folder
```

其中：

- *user_goup* 为当前用户的用户组
- *user_name* 为当前用户名
- *synced_folder* 为需要同步的文件夹

如果需要使用当前用户来运行 Sync，需要编辑 **/usr/lib/systemd/user/resilio-sync.service** 并更改  "WantedBy=multi-user.target" 为 "WantedBy=default.target"，保存。 以 *--user* 参数开启服务：

```bash
systemctl --user enable resilio-sync
```

运行参数有 *start, stop, enable, disable, status* 。
例如在当前用户下启动 **Sync**：

```bash
systemctl --user start resilio-sync
```

### 卸载

```bash
sudo apt-get purge resilio-sync
```