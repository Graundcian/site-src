---
title: "Typora图片自动上传图床"
date: 2021-05-15T23:46:23+08:00
draft: false
toc: true
authors: [graundcian]
tags: [Typora, PicGo-Core]
---
PicGo-Core配置 Github 图床、下载插件、手动配置Config.json(配置文件)、图片时间戳命名

<!--more-->

# 下载PicGo-Core

![img](https://cdn.jsdelivr.net/gh/Graundcian/images@master/blog/2021/05/16/20210516235109)

![img](https://cdn.jsdelivr.net/gh/Graundcian/images@master/blog/2021/05/16/20210516235128)

![img](https://cdn.jsdelivr.net/gh/Graundcian/images@master/blog/2021/05/16/20210516235143)

**注意**：图片中“对网络位置的图片应用上述规则”这个选项。

- 如果不勾选，从其他网站复制的图片，就不会上传至你配置的图床，md文档中会直接显示对应网站图片链接；

- 如果勾选了，就会在本地生成upload文件夹，自动下载图片后，再上传至你配置的图床。

- 无论是否勾选，对于QQ截屏的图片，也会在本地生成upload文件夹，保存图片后，再上传至你配置的图床。

# 配置PicGo-Core

以 Github 作为图床。

## 安装 Node.js

下载 PicGo 插件，需要 nodejs 的运行环境。

- Nodejs下载地址：https://nodejs.org/en/

## 安装插件

- [github-plus](https://github.com/zWingz/picgo-plugin-github-plus) ：An **uploader** for GitHub & Gitee with sync function.
-  [super-prefix](https://github.com/gclove/picgo-plugin-super-prefix#readme) ：A plugin for customizing images filename and prefix.

```bash
cd C:\Users\aji\AppData\Roaming\Typora\picgo\win64

.\picgo.exe install gitee-uploader

.\picgo.exe install super-prefix
```



## 修改配置文件

![image-20210517001737927](https://cdn.jsdelivr.net/gh/Graundcian/images@master/blog/2021/05/17/20210517001739.png)



配置文件 config.json

```json
{
  "picBed": {
    "current": "github",
    "uploader": "github", // 代表当前的上传图床
    "transformer": "path",
    "github": {
      "branch": "master", // 分支名，默认是 master
      "customUrl": "",// 自定义访问链接，例如：CDN加速 https://cdn.jsdelivr.ne
      "path": "", // 自定义存储路径，比如 img/ 建议填
      "repo": "", // 仓库名，格式是 username/reponame 必填
      "token": ""
    }
  },
  "picgoPlugins": {
    "picgo-plugin-super-prefix": true,
    "picgo-plugin-github-plus": true
  }, // 为插件预留
  "picgo-plugin-super-prefix": {
    "prefixFormat": "YYYY/MM/DD/",
    "fileFormat": "YYYYMMDDHHmmss"
  } //super-prefix插件配置
}
```

## 图片上传验证

![image-20210517001737927](https://cdn.jsdelivr.net/gh/Graundcian/images@master/blog/2021/05/17/20210517001739.png)

![img](https://cdn.jsdelivr.net/gh/Graundcian/images@master/blog/2021/05/17/20210517002427)



# 参考文档

- [Upload Images (typora.io)](https://support.typora.io/Upload-Image/#install-prebuilt-binary-of-picgo-core-linux--windows)
- [Typora自动上传图片配置，集成PicGo-Core，文件以时间戳命名]([Typora自动上传图片配置，集成PicGo-Core，文件以时间戳命名_in_the_road的博客-CSDN博客](https://blog.csdn.net/in_the_road/article/details/105733292))



