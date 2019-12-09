---
title: 初识nginx
date: 2019-12-07 17:03:21
tags: nginx
categories:
 - [nginx学习笔记]
---

## 1. Nginx的三个主要应用场景
- 静态资源服务
    通过本地文件系统提供服务
- 反向代理服务
    - Nginx强大的性能
    - 缓存
    - 负载均衡
- API服务
    OpenResty

## 2. Nginx主要优点
- 高并发高性能
- 可扩展性好
- 高可靠性
- 热部署
- SBD许可证(可修改源码商用)

## 3. Nginx组成
- Nginx二进制可执行文件
- Nginx.conf配置文件
- access.log访问日志
- error.log错误日志

## 4. 编译安装Nginx
### 4.1 第一步：准备工作
在[官网](http://nginx.org/en/download.html)下载源码，选择最新[稳定版](http://nginx.org/download/nginx-1.16.1.tar.gz)，linux可使用wget下载。
```bash
cd /usr/local
wget http://nginx.org/download/nginx-1.16.1.tar.gz
tar xzf nginx-1.16.1.tar.gz
cd nginx-1.16.1
```

编译Nginx需要安装一些依赖工具。
```bash
yum -y install gcc zlib zlib-devel pcre-devel openssl openssl-devel
```
### 4.2 编译安装
- 源码目录结构：
```bash
 auto   #编译配置相关文件 
 CHANGES #更新记录
 CHANGES.ru #更新记录俄语版
 conf #Nginx示例配置
 configure #配置命令
 contrib #vim语法高亮脚本
 html #访问的默认html
 LICENSE #许可证
 man #man命令文档
 README 
 src #源码目录
```

- 配置：
```bash
cd nginx-1.16.1 #进入目录
./configure --help #查看自定义配置帮助
./configure --with-http_v2_module #配置，且使用http2模块
```

- 编译安装
```bash
make #编译
make install #安装，默认安装在/usr/local目录下

cd /usr/local/nginx/sbin/ && ./nginx #启动nginx

./nginx -s reload #重载配置文件
./nginx -s stop #立刻关闭nginx
./nginx -s quit #优雅退出
./nginx -t #测试配置文件是否正确
./nginx -s reopen #日志切割
```

- 设置开机启动
```bash
vim /etc/rc.local 
```
然后在底部增加 /usr/local/nginx/sbin/nginx，即可开机启动

