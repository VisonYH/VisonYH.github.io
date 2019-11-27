---
title: 利用hexo、travis-ci打造专属博客
toc: true
comment: on
donate: true
tags:
 - 博客
 - hexo
 - travis-ci
categories:
 - [博客]
---

## 1. hexo篇
### 1.1 hexo是什么？
hexo是一个快速、简洁且高效的博客框架，通过一些预设的模板以及资源文件，将markdown等文件渲染成html页面。具有以下特点：
- 作为npm包，安装、使用很方便；
- 插件较多、主题多样，配置简单；
- 部署方便，可以将生成的博客页面直接上传到github或其他仓库；

### 1.2 hexo的常用配置及操作
#### 1.2.1 hexo目录结构

通过hexo初始化博客站点之后，将生成如下的目录结构：

```
├── _config.yml     //整个站点的配置中心，可以配置大部分参数，后面会详细说明
├── package.json
├── scaffolds       //模板文件，对应有draft.md、page.md和post.md
├── source          //博客源文件(写博客的地方)
|   ├── _drafts     //草稿，通过hexo publish可以将草稿发布
|   └── _posts      //正式文章，Markdown 和 HTML 文件会被解析并放到 public 文件夹
└── themes          //主题，主题一般从github下载而来，一个主题对应一个文件夹
```

#### 1.2.2 hexo常用命令

```bash
clean     //清除产生的文件缓存，有时修改文件了hexo g不生效时可以试试。
config    //获取和设置hexo配置
deploy    //根据配置文件部署站点
generate  //生成静态html博客页面
help      //程序员都知道
init      //新建一个博客站点
list      //显示本博客站点的信息
migrate   //将其他站点迁移到hexo
new       //新建文章
publish   //将草稿文件夹内的草稿移至文章文件夹内，hexo g时将对其生效
render    //Render files with renderer plugins.
server    //起一个本地server，用来预览文章
version   //显示hexo及各库的版本信息
```

#### 1.2.3 配置文件选项
一般在_config.yml中进行配置，由于配置项较多，且大多数都是直接使用默认值，需要改变的配置在下文会有详细说明，这里不再赘述，参见[传送门](https://hexo.io/zh-cn/docs/configuration)。



-------------