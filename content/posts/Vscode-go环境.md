---
title: 'VScode Go环境配置'
date: 2019-11-03 22:14:16
toc: true
authors: [graundcian]
tags: [ VScode, Golang]

---

Go语言环境配置

<!--more-->

## 准备

目录切换：

```bash
cd %GOPATH%\src\github.com\golang
```

如果src目录下面没有github.com\golang请自行创建
完成目录切换后，开始下载插件包：

```bash
git clone https://github.com/golang/tools.git tools

```

当下载完成后，你会发现%GOPATH%\src\github.com\golang多了一个tools目录
需要把tools目录下的所有文件拷贝到%GOPATH%\src\golang.org\x\tools下，如果没有自行创建
当然如果是windows环境，如果你当前是在%GOPATH%\src\golang.org\x\tools
目录下，可以直接使用如下命令进行拷贝

```powershell
copy /s /e %GOPATH%\src\github.com\golang\tools
```

直接将下载的tools目录下的所有文件拷贝到%GOPATH%\src\golang.org\x\tools目录下

经过多次测试，插件中有几个其实不用翻墙或其他方法就可以安装成功：
github.com/nsf/gocode
github.com/uudashr/gopkgs/cmd/gopkgs
github.com/fatih/gomodifytags
github.com/haya14busa/goplay/cmd/goplay
github.com/derekparker/delve/cmd/dlv

## 安装

下面安装无法安装的插件
开始安装：
切换到GOPATH目录下，执行相关的go install 命令

```bash
go install golang.org/x/lint/
go install github.com/ramya-rao-a/go-outline

go install github.com/acroca/go-symbols

go install golang.org/x/tools/cmd/guru

go install golang.org/x/tools/cmd/gorename

go install github.com/josharian/impl

go install github.com/rogpeppe/godef

go install github.com/sqs/goreturns

go install github.com/golang/lint/golint

go install github.com/cweill/gotests/gotests
```

## golint需要单独安装

切换目录到%GOPATH%\src\golang.org\x, 执行：

```bash
git clone https://github.com/golang/lint.git

```

```bash
cd lint/golint/
go install
```

这样vscode下go开发需要安装的插件都已经安装成功。

