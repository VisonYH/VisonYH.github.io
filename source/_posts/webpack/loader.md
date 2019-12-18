---
title: 编写webpack loader
date: 2019-12-16 20:15:23
tags:
 - webpack
 - loader
---

## webpack loader是什么？
webpack loader是用来处理webpack模块的函数。在webpack中，一切皆函数，js文件、图片、css文件都被webpack作为模块来打包。webpack本身一开始也就是个打包工具，只不过现在功能早已不局限在模块的打包了。loader就是webpack功能拓展的重要组成部分，用来对每个模块在打包时进行处理。实际上每个loader就是一个函数，其输入为对应的模块代码，输出为相应的处理之后的结果。

## webpack loader配置
典型的webpack loader配置如下：
```javascript
 module: {
    rules: [{
        // 正则匹配该loader对应的模块，匹配到模块文件的将被该loader处理
        test: /\.jsx?$/,
        // 这里是匹配条件，每个选项都接收一个正则表达式或字符串
        // test 和 include 具有相同的作用，都是必须匹配选项
        // exclude 是必不匹配选项（优先于 test 和 include）
        // 最佳实践：
        // - 只在 test 和 文件名匹配 中使用正则表达式
        // - 在 include 和 exclude 中使用绝对路径数组
        // - 尽量避免 exclude，更倾向于使用 include
        include: [
          path.resolve(__dirname, "app")
        ],
        exclude: [
          path.resolve(__dirname, "app/demo-files")
        ],
        loader: "babel-loader",
        // 配置loader参数，在loader中可以拿到这些参数  
        options: {
          presets: ["es2015"]
        },
      }
    ]
 }
```


## webpack loader生命周期



## webpack loader编写

