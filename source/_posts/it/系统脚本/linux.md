# du 查看文件大小 
## 查看文件夹大小 
``` 
    du -h --max-depth=1 
    du -sh path  
```
# df 查看磁盘大小
```
    df -sh 
```
# zip 命令 
## 压缩
> 压缩当前目录到 myfile.zip
``` zip -r myfile.zip ./* ```
## 解压
> 解压myfile.zip到指定文件夹
```unzip -o -d /home/sunny myfile.zip```
## 操作
```
-r:压缩文件夹
-o:不提示的情况下覆盖文件；
-d:指明将文件解压缩到指定目录下；
```
# Rsync 同步推送
## 本地同步到远程，推
```rsync -avH  /data/test.php root@192.168.1.200:/path/```
## 远程同步到本地，拉
```rsync -avH  root@192.168.1.200:/path/200.php  /data/ ```
## 指定端口
```
Rsync -avH -e 'ssh -p 58822' 本地文件路径 root@172.16.16.241:/home/tomcat-wpn/webapps/waimai/
```
## 本地比对差异不复制
```rsync -avhn gs webapps/gs > ./log.txt```
## help
```
rsync 命令
rsync 是一个功能非常强大的工具，其命令也有很多功能选项。rsync 的命令格式为：

1）本地使用：
rsync [OPTION...] SRC... [DEST]

2）通过远程 Shell 使用：
拉: rsync [OPTION...] [USER@]HOST:SRC... [DEST]
推: rsync [OPTION...] SRC... [USER@]HOST:DEST

3）访问 rsync 服务器:
拉: rsync [OPTION...] [USER@]HOST::SRC... [DEST]
推: rsync [OPTION...] SRC... [USER@]HOST::DEST
拉: rsync [OPTION...] rsync://[USER@]HOST[:PORT]/SRC... [DEST]
推: rsync [OPTION...] SRC... rsync://[USER@]HOST[:PORT]/DEST
其中：

SRC: 是要复制的源位置
DEST: 是复制到目标位置
若本地登录用户与远程主机上的用户一致，可以省略 USER@
使用远程 shell 同步时，主机名与资源之间使用单个冒号“:”作为分隔符
使用 rsync 服务器同步时，主机名与资源之间使用两个冒号“::”作为分隔符
当访问 rsync 服务器时也可以使用 rsync:// URL
“拉”复制是指从远程主机复制文件到本地主机
“推”复制是指从本地主机复制文件到远程主机
当进行“拉”复制时，若指定一个 SRC 且省略 DEST，则只列出资源而不进行复制
下面列出常用选项：

选项	说明
-a, ––archive	归档模式，表示以递归方式传输文件，并保持所有文件属性，等价于 -rlptgoD (注意不包括 -H)
-r, ––recursive	对子目录以递归模式处理
-l, ––links	保持符号链接文件
-H, ––hard-links	保持硬链接文件
-p, ––perms	保持文件权限
-t, ––times	保持文件时间信息
-g, ––group	保持文件属组信息
-o, ––owner	保持文件属主信息 (super-user only)
-D	保持设备文件和特殊文件 (super-user only)
-z, ––compress	在传输文件时进行压缩处理
––exclude=PATTERN	指定排除一个不需要传输的文件匹配模式 
––exclude "source"
––exclude-from=FILE	从 FILE 中读取排除规则
––include=PATTERN	指定需要传输的文件匹配模式
––include-from=FILE	从 FILE 中读取包含规则
––copy-unsafe-links	拷贝指向SRC路径目录树以外的链接文件
––safe-links	忽略指向SRC路径目录树以外的链接文件（默认）
––existing	仅仅更新那些已经存在于接收端的文件，而不备份那些新创建的文件
––ignore-existing	忽略那些已经存在于接收端的文件，仅备份那些新创建的文件
-b, ––backup	当有变化时，对目标目录中的旧版文件进行备份
––backup-dir=DIR	与 -b 结合使用，将备份的文件存到 DIR 目录中
––link-dest=DIR	当文件未改变时基于 DIR 创建硬链接文件
––delete	删除那些接收端还有而发送端已经不存在的文件
––delete-before	接收者在传输之前进行删除操作 (默认)
––delete-during	接收者在传输过程中进行删除操作
––delete-after	接收者在传输之后进行删除操作
––delete-excluded	在接收方同时删除被排除的文件
-e, ––rsh=COMMAND	指定替代 rsh 的 shell 程序
––ignore-errors	即使出现 I/O 错误也进行删除
––partial	保留那些因故没有完全传输的文件，以是加快随后的再次传输
––progress	在传输时显示传输过程
-P	等价于 ––partial ––progress
––delay-updates	将正在更新的文件先保存到一个临时目录（默认为 “.~tmp~”），待传输完毕再更新目标文件
-v, ––verbose	详细输出模式
-q, ––quiet	精简输出模式
-h, ––human-readable	输出文件大小使用易读的单位（如，K，M等）
-n, ––dry-run	显示哪些文件将被传输
––list-only	仅仅列出文件而不进行复制
––rsyncpath=PROGRAM	指定远程服务器上的 rsync 命令所在路径
––password-file=FILE	从 FILE 中读取口令，以避免在终端上输入口令，通常在 cron 中连接 rsync 服务器时使用
-4, ––ipv4	使用 IPv4
-6, ––ipv6	使用 IPv6
––version	打印版本信息
––help	显示帮助信息
```

# 重启网络服务

## Mac

```Bash
sudo ifconfig en0 down
sudo ifconfig en0 up
```

## Linux

```
/etc/init.d/networking restart
```

