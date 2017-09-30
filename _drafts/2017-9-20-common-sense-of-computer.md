---
layout: post
title:  "一些计算机常识"
date:   2017-9-20
categories: my blog
---

## 路径符号

`/` : /home/doc/ 正斜杠 常见于Unix/Linux

`\` : C:\Windows\System 反斜杠 常见于Windows

`\\` : C:\\Windows\\System 相当于 C:/Windows/System ，由于`\`在C语言中是转义符，所以`\\`转义后为`\`。而单独写`\`是会出错的，因为实际上写的是一个转义符，甚至跟在转义符后的字符会被转义。

`./` : 当前目录

`../` : 当前目录的上级目录

### 历史：

Windows 用反斜杠（“\”）的历史来自 DOS，而 DOS 的另一个传统是用斜杠（“/”）表示命令行参数，比如：cd %SystemDrive%dir /s /b shell32.dll既然 DOS 这边斜杠被占用了，只好找一个最接近的。那就是它了。而在 UNIX 环境中，我们用减号（“-”）和双减号（“--”）表示命令行参数。用斜杠表示命令行参数是兼容性原因。这个问题最初起源自 IBM。IBM 在最初加入 DOS 开发时贡献了大批工具，它们都是用斜杠处理命令行参数的。而这个传统源自于 DEC/IBM，比如当年的 VMS 就是用斜杠处理命令行参数，它的目录分隔符是美元符（“$”）。顺便说一句，这个传统也被部分地继承进了 DOS 和 Windows 体系，日文版的 Windows 就把反斜杠在屏幕上显示为“¥”，虽然实际上还是反斜杠。如今的 Windows 内核在处理路径时确实可以同时支持斜杠和反斜杠。很多时候我们看到用斜杠时出错，是因为应用程序层面的原因。比如 cmd.exe 就不支持用斜杠表示路径，而PowerShell.exe 支持，也正因为这个原因，PowerShell 开始转而使用减号作为命令行参数的起始符。（知乎 - <a href="https://www.zhihu.com/question/19970412/answer/15479052">陈甫鸼</a>）

## Windows常用命令行命令

`cd [path] ` 进入目录

`md [dir]` 创建目录

`rm [dir]` 删除目录

`type nul > [file.suffix]` 创建文件

`copy [orgin file] [new file]` 复制文件

`del [filename]` 删除文件

`ren [filename] [new filename]` 重命名文件

`copy nul [filename]` -> `del [filename]` 粉碎文件

`get-item -path env:*` 查看所有环境变量