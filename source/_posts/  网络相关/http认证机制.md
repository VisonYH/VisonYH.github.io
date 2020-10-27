---
title: Http认证机制
toc: true
comment: on
donate: true
tags:
 - HTTP
 - 网络
 - 认证
 - 鉴权
categories:
 - [博客]
---

> “HTTP/1.0” 包含了一种以 “用户名 + 密码” 的明文传输的访问认证规范，称之为“Basic Auth”，在没有类似ssl层保护的情况下，这种方案是很不安全的。后来，在此基础上引入了密码学的加密理论，“密码”通过加密后不再明文传输，演变为所谓的”Digest Access Authentication“。

### Basic Auth

![img](https://mdn.mozillademos.org/files/14689/HTTPAuth.png)


