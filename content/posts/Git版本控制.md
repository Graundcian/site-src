---
title: "Git版本控制"
authors: [graundcian]
date: 2019-07-15 16:02:53
toc: true
draft: false
tags: [git,linux]
---

Git的基本配置、设置代理

<!--more-->

### 用户信息

```bash
git config --global user.name "runoob"
git config --global user.email test@runoob.com
```

### 远程仓库

#### 添加远程

```bash
git remote add origin git@github.com:tianqixin/runoob-git-test.git
# 初次提交
git push -u origin master 
# 之后提交
git push
```

#### 查看当前远程库

```bash
$ git remote
origin
$ git remote -v
origin    git@github.com:tianqixin/runoob-git-test.git (fetch)
origin    git@github.com:tianqixin/runoob-git-test.git (push)
```

   执行时加上 -v 参数，你还可以看到每个别名的实际链接地址

#### 提取远程仓库

1. 从远程仓库下载新分支与数据：

```bash
git fetch
```

2. 从远端仓库提取数据并尝试合并到当前分支：

```bash
git merge
```

#### 删除远程仓库

```bash
git remove [别名(origin)]
```

### 代理

#### 全局代理

```bash
git config --global http.proxy 'socks5://127.0.0.1:1080'
git config --global https.proxy 'socks5://127.0.0.1:1080'
```

```bash
git config --global http.proxy 'http://127.0.0.1:1080'
git config --global https.proxy 'http://127.0.0.1:1080'
```

#### 取消代理

```bash
git config --global --unset http.proxy
git config --global --unset https.proxy
```

#### 只对github.com

```bash
git config --global http.https://github.com.proxy socks5://127.0.0.1:1080
```

#### 取消代理

```bash
git config --global --unset http.https://github.com.proxy
```
