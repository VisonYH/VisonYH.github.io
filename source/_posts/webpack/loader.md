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

![webpack loader生命周期](/img/webpack学习笔记/webpack-loader执行过程.png)
## webpack loader编写
以编写一个config-loader为例，实现.config文件的解析和加载。

假设有这样一个.config文件：
```bash
API_PATH /api/
IMG_PATH /assets/image/
HOST www.example.com
```

通过代码```const { API_PATH } = require("/path/to/.config")```可以实现将该文件解析成javascript对象，轻松获取每一项配置。

config-loader.js代码：
```javascript
// 用来获取webpack config文件中配置的loader options选项
const loaderUtils = require('loader-utils');
// 用来验证配置的正确性
const validateOptions = require('schema-utils');

const schema = {
    type: 'object',
    properties: {
        test: {
            type: 'string'
        }
    }
};
module.exports = function (source) {
    // 获取配置项
    const options = loaderUtils.getOptions(this);

    validateOptions(schema, options, 'Example Loader');
    // source 为匹配上的文件，编写loader的本质就是对source进行处理，以下是对source进行处理的过程
    source = source.split('\n').filter(item => {
        item = item.trim();
        return /^[a-zA-Z]/.test(item);
    })
    let configs = source.reduce((prev, item) => {
        item = /^(\w+)\s+(\.+)/g.exec(item);
        if (item) {
            prev[item[1]] = item[2]
        }
        return prev
    }, {})
    // 同步loader可以通过this.callback()或直接return返回处理好的结果
    this.callback(null, `module.exports=${JSON.stringify(configs)}`);
    // 异步loader需要通过调用this.async()获取callback函数，再将处理后的内容返回
    // 注意：一定要在异步代码之后执行this.async(),不然默认直接返回了
    // const callback = this.async();
    // callback(null, `module.exports=${JSON.stringify(configs)}`);
}
```

webpack规则配置：
```javascript
module: {
    rules: [{
        test: /\.config$/,
        use: [{
            loader: path.resolve('path/to/your-loader'), //替换成本地的loader路径
        }],
        exclude: /node_modules/
    }]
}
```