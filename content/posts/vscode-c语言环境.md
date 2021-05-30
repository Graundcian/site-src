---
title: 'Vscode C语言环境'
toc: true
authors: [graundcian]
date: 2020-04-11 04:50:33
tags: [C,VScode]
---
VS code中的配置C语言环境。
<!--more-->

## 安装MinGW-w64
- [下载](https://sourceforge.net/projects/mingw-w64/files/Toolchains%20targetting%20Win64/Personal%20Builds/mingw-builds/8.1.0/threads-posix/seh/x86_64-8.1.0-release-posix-seh-rt_v6-rev0.7z/download)安装

### 环境变量配置
- **PATH** 中添加 xxx\mingw64\bin
- 新建 **INCLUDE**变量，值为xxx\mingw64\include

## 安装VScode

### 安装code runner扩展

### 配置文件

新建项目目录，用VScode打开此目录，目录下会产生 **.vscode** 目录，在 **.vscode** 下新建三个 josn 文件。

#### No.1 launch.json

```json
{
    "version": "0.2.0",  
    "configurations": [  
        {  
            "name": "(gdb) Launch", // 配置名称，将会在启动配置的下拉菜单中显示
            "type": "cppdbg",       // 配置类型，这里只能为cppdbg
            "request": "launch",    // 请求配置类型，可以为launch（启动）或attach（附加）  
            "program": "${workspaceFolder}/${fileBasenameNoExtension}.exe",// 将要进行调试的程序的路径  
            "args": [],             // 程序调试时传递给程序的命令行参数，一般设为空即可  
            "stopAtEntry": false,   // 设为true时程序将暂停在程序入口处，一般设置为false  
            "cwd": "${workspaceFolder}", // 调试程序时的工作目录，一般为${workspaceFolder}即代码所在目录  
            "environment": [],  
            "externalConsole": true, // 调试时是否显示控制台窗口，一般设置为true显示控制台  
            "MIMode": "gdb",  
            "miDebuggerPath": "xxx\\mingw64\\bin\\gdb.exe", // miDebugger的路径，注意这里要与MinGw的路径对应  
            "preLaunchTask": "gcc", // 调试会话开始前执行的任务，一般为编译程序，c++为g++, c为gcc  
            "setupCommands": [  
                {   
            "description": "Enable pretty-printing for gdb",  
                    "text": "-enable-pretty-printing",  
                    "ignoreFailures": true  
                }  
            ]  
        }  
    ]  
}

```

#### No.2 tasks.json

```json
{
    // 有关 tasks.json 格式的参考文档：https://go.microsoft.com/fwlink/?LinkId=733558 。
    "version": "2.0.0",
    "tasks": [{
        "label": "gcc",
        "type": "shell", // { shell | process }
        // 适用于 Windows 的配置：
        "windows": {
            "command": "gcc",
            "args": [
                "-g",
                "\"${file}\"",
                "-o",
                "\"${fileDirname}\\${fileBasenameNoExtension}.exe\""
                // 设置编译后的可执行文件的字符集为 GB2312：
                // "-fexec-charset", "GB2312"
                // 直接设置命令行字符集为 utf-8：
                // chcp 65001
            ]
        },
        // 定义此任务属于的执行组：
        "group": {
            "kind": "build", // { build | test }
            "isDefault": true // { true | false }
        },
        // 定义如何在用户界面中处理任务输出：
        "presentation": {
            // 控制是否显示运行此任务的面板。默认值为 "always"：
            // - always:    总是在此任务执行时显示终端。
            // - never:     不要在此任务执行时显示终端。
            // - silent:    仅在任务没有关联问题匹配程序且在执行时发生错误时显示终端
            "reveal": "silent",
            // 控制面板是否获取焦点。默认值为 "false"：
            "focus": false,
            // 控制是否将执行的命令显示到面板中。默认值为“true”：
            "echo": false,
            // 控制是否在任务间共享面板。同一个任务使用相同面板还是每次运行时新创建一个面板：
            // - shared:     终端被共享，其他任务运行的输出被添加到同一个终端。
            // - dedicated:  执行同一个任务，则使用同一个终端，执行不同任务，则使用不同终端。
            // - new:        任务的每次执行都使用一个新的终端。
            "panel": "dedicated"
        },
        // 使用问题匹配器处理任务输出：
        "problemMatcher": {
            // 代码内问题的所有者为 cpp 语言服务。
            "owner": "cpp",
            // 定义应如何解释问题面板中报告的文件名
            "fileLocation": [
                "relative",
                "${workspaceFolder}"
            ],
            // 在输出中匹配问题的实际模式。
            "pattern": {
                // The regular expression.
                "regexp": "^(.*):(\\d+):(\\d+):\\s+(warning|error):\\s+(.*)$",
                // 第一个匹配组匹配文件的相对文件名：
                "file": 1,
                // 第二个匹配组匹配问题出现的行：
                "line": 2,
                // 第三个匹配组匹配问题出现的列：
                "column": 3,
                // 第四个匹配组匹配问题的严重性，如果忽略，所有问题都被捕获为错误：
                "severity": 4,
                // 第五个匹配组匹配消息：
                "message": 5
            }
        }
    }]
}

```

#### No.3 setting.json

```json
{
    "files.associations": {
        "tidl_alg_int.h": "c",
        "limits": "c"
    }
}

```