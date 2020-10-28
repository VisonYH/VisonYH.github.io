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

#### 1.认证过程

​    mdn文档给出的图清晰明了，认证过程如下图所示。客户端需要在请求头中添加`Authorization: Basic base64_encode(user:pass)”`字段，服务端对此进行校验，校验失败即返回403。如请求头中未包含该字段，则返回401。

![img](/Users/sunwei/Documents/visonyh.github.io/source/img/HTTPAuth.png)

#### 2. Basic Auth 请求头的生成

​    前面说到，Basic Auth的请求头格式为`Authorization: Basic base64_encode(user:pass)”`。首先，`Authorization`是`HTTP`协议用来认证的首部字段，`Basic`是`Authorization`的一种类型，代表Basic Auth。 后面的一串字符编码代表的是将用户名和密码以`user:pass`格式组成字符串，再利用base64进行编码。以JavaScript的npm包[js-base64](https://www.npmjs.com/package/js-base64)为例，使用如下：

```javascript
import { Base64 } from 'js-base64';
let nonceStr = Base64.encode(`${name}:${pass}`);
// 请求头格式为: `Authorization: Basic ${nonceStr}`
```

​    服务端拿到Authorization首部字段后，利用base64反编码即可得到用户名密码，再查询数据库进行校验即可进行权限校验。服务端以node.js的`basic-auth`包为例。

```javascript
var auth = require('basic-auth');
var user = auth(req)
// => { name: 'something', pass: 'whatever' }
// 拿到name和pass后即可进行权限校验
```



