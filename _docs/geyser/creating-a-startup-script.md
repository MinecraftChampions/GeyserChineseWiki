---
title: 创建Geyser独立版启动脚本
---

# 为Geyser独立版创建启动脚本

**请安装Java16及以上版本的Java**

下载Geyser后将它丢到一个目录下,编写启动脚本启动,类似(Bukkit/Spigot/Paper/BungeeCord/Velocity)一样,java启动程序的命令

### Windows
* 在和Geyser-Standalone相同的目录下新建一个文本文档并重命名为`run.bat`. 使用文本编辑器打开,并输入以下内容:
```batch
@echo off
java -Xms1024M -jar Geyser-Standalone.jar
pause
```
* 双击 **run.bat** 以运行, 然后Geyser就启动了. Geyser会在它所在的目录下生成所需的文件


### macOS
* 在和Geyser-Standalone相同的目录下新建一个文本文档并重命名为`run.command`. 使用文本编辑器打开,并输入以下内容:
```sh
#!/bin/bash 
cd "$( dirname "$0" )" 
java -Xms1024M -jar Geyser-Standalone.jar
```
* 打开终端, 输入 `chmod a+x` **(不要回车!)**, 然后把 *run.command* 文件拖进来.
* 回车,启动. Geyser会在它所在的目录下生成所需的文件


### Linux
* 在和Geyser-Standalone相同的目录下新建一个文本文档并重命名为`run.sh`. 使用文本编辑器打开,并输入以下内容:
```sh
#!/bin/sh 
cd "$( dirname "$0" )" 
java -Xms1024M -jar Geyser-Standalone.jar
```
* 打开终端,运行命令 `chmod +x ~(dir)/run.sh`,其中 `dir` 是 Geyser 所在的文件夹名.这个命令会将 run.sh 文件的权限设置为可执行.
* 然后,输入 `./run.sh`来运行 Geyser. Geyser会在它所在的目录下生成所需的文件






