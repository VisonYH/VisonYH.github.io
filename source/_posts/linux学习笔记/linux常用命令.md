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

shutdown -h now #关机
reboot -h now #重启机器
```

###linux程序启动的三种方式
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
