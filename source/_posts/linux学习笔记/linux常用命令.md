---
title: linux常用命令
date: 2019-12-02 14:31:40
tags:
categories:
 - [linux学习笔记]
---

```bash
passwd #修改当前用户密码

useradd xxx #添加xxx用户
passwd xxx #修改xxx用户密码

rpm -qa #查看已安装的软件列表
rpm -e #删除软件erase
rpm -r #删除软件remove

yum install xxx #使用yum安装软件
yum erase xxx #使用yum卸载软件

#设置环境变量
export xxx_HOME=/xxx/xxx 
export PATH=$xxx_HOME/bin:$PATH

ls -lh #以M为单位显示文件大小


shutdown -h now #关机
reboot -h now #重启机器
```

文件打包压缩相关
```bash
tar xzvf xxx xxx1 #将xxx解压到xxx1
tar czf xxx1 xxx #将xxx打包到xxx1，并且以gzip压缩
tar cjf xxx1 xxx #将xxx打包到xxx1，并且以bz2压缩
-c #建立新的压缩文件
-r #添加文件到已经压缩的文件
-u #添加改变了和现有的文件到已经存在的压缩文件
-x #从压缩的文件中提取文件
-t #显示压缩文件的内容
-z #支持gzip解压文件
-j #支持bzip2解压文件
-v #显示操作过程
-k #保留源有文件不覆盖
-C #切换到指定目录
-f #指定压缩文件
```

### linux程序启动的三种方式
- shell交互命令行启动
在对应目录下，运行```./filename```即可执行，如已设置环境变量，可以不用```./```。
- 后台运行
```bash
nohup /xxxDir/xxx >/dev/null 2>&1 &
```
- 以服务运行
```bash
systemctl start xxx #启动xxx服务
ststemctl enable xxx #设置开机启动
```
