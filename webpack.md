# webpack

> 模块化编程工具，通过npm安装

## webpack和grunt、gulp有什么区别？

* Grunt和Gulp的工作方式是：在一个配置文件中，指明对某些文件进行类似编译，组合，压缩等任务的具体步骤，这个工具之后可以自动替你完成这些任务。

* Webpack的工作方式是：把你的项目当做一个整体，通过一个给定的主文件（如：index.js），Webpack将从这个文件开始找到你的项目的所有依赖文件，使用loaders处理它们，最后打包为一个浏览器可识别的JavaScript文件。

* 相对来说，webpack更方便更快捷，能打包更多文件。

### 安装

```
// 接管
npm init;
```

> 必须全局安装才能执行webpack，否则找不到指定的命令。

```
//全局安装
npm install -g webpack
//安装到你的项目目录
npm install --save-dev webpack
```

### 执行webpack

#### 1. 命令行执行

```
// 局部
.\node_modules\.bin\webpack app/index.js dist/bundle.js
// 全局
webpack app/index.js dist/bundle.js
// webpack命令 入口 出口
```

#### 2. 配置文件执行

根目录下创建webpack.config.js文件，规范代码如下：

```
var path = require('path');

module.exports = {
  // 入口
  entry: './app/index.js',
  // 出口
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist')
  }
};
```

通过命令行执行此文件即可。

```
webpack --config webpack.config.js
```

#### 3. 设置快捷方式

在package.json文件的scripts中加入快捷方式：

```
"build": "webpackapp/index.js dist/bundle.js"
```

执行如下命令即可。

```
npm build
```

### css-loader，style-loader使用

* 安装css-loader,style-loader

```
// 尝试过同时安装，会报错
npm install css-loader --save-dev
npm install style-loader --save-dev
```

> 不能重复安装

* 创建几个文件，下列为几个文件的相对路径

```
- index.html
- main.js
- app.css
- package.json
- webpack.config.js  // 配置文件，自己编写
```

* 各个文件分别写入各自的代码块。

```
/* index.html */

<html>
  <head>
    <script type="text/javascript" src="bundle.js"></script>
  </head>
  <body>
    <div id="test">Hello World</div>
  </body>
</html>


/* main.js */

// 引入app.css
require('./app.css');


/* app.css */

#test{
  background:red;
  width:100px;
  height:100px;
  color:blue;
}


/* webpack.config.js */

module.exports = {
  // 入口文件
  entry: './main.js',
  // 出口文件
  output: {
    filename: 'bundle.js'
  },
  // 处理
  module: {
    loaders:[
      { test: /\.css$/, loader: 'style-loader!css-loader' },
    ]
  }
};
```

* 最后执行配置文件，就成功了。

```
webpack --config webpack.config.js
```

### less-loader

* 安装less-loader 

```
npm install less --save-dev
npm install less-loader --save-dev
```

* 创建index.less文件。
* 在webpack.config.js中改变处理。

```
{test: /\.less$/, loader: 'style-loader!css-loader!less-loader'},
```

* 在main.js中引入.less文件即可。

```
require('./index.less');
```

* 执行配置文件，完成操作。

```
webpack --config webpack.config.js
```

### url-loader

> 使用方式同上

### file-loader

> 使用方式同上

### json-loader

> 使用方式同上

### raw-loader

> 使用方式同上

### babel-loader

> 处理js文件



