# webpack

## 五大核心概念

1、entry

​	  入口    (Entry)    指示     webpack     以哪个文件为入口起点开始打包， 分析构建内部依赖图。  

2、output

​	  输出    (Output)    指示     webpack     打包后的资源     bundles     输出到哪里去， 以及如何命名  

3、loader

​	  Loader让 webpack能 够 去 处 理 那 些 非JavaScript文 件(webpack自 身 只 理 解JavaScript）

4、plugins

​	  插件(Plugins)可以用于执行范围更广的任务。插件的范围包括，从打包优化和压缩， 一直到重新定义环境中的变量等。 

5、mode

​	开发环境：development

​	生产环境：production

## 初始化配置

初始化package.json

​	npm init

下载webpack

​	npm install webpack webpack-cli -g

​	npm install webpack webpack-cli -D

```JavaScript
/*
  webpack.config.js  webpack的配置文件
    作用: 指示 webpack 干哪些活（当你运行 webpack 指令时，会加载里面的配置）

    所有构建工具都是基于nodejs平台运行的~模块化默认采用commonjs。
*/

// resolve用来拼接绝对路径的方法
const { resolve } = require('path');

module.exports = {
  // webpack配置
  // 入口起点
  entry: './src/index.js',
  // 输出
  output: {
    // 输出文件名
    filename: 'bundle.js',
    // 输出路径
    // __dirname nodejs的变量，代表当前文件的目录绝对路径
    path: resolve(__dirname, 'build')
  },
  // loader的配置
  module: {
    rules: [
      // 详细loader配置
      // 不同文件必须配置不同loader处理
      {
        // 匹配哪些文件
        test: /\.css$/,
        // 使用哪些loader进行处理
        use: [
          // use数组中loader执行顺序：从右到左，从下到上 依次执行
          // 创建style标签，将js中的样式资源插入进行，添加到head中生效
          'style-loader',
          // 将css文件变成commonjs模块加载js中，里面内容是样式字符串
          'css-loader'
        ]
      }
    ]
  },
  // plugins的配置
  plugins: [
    // 详细plugins的配置
  ],
  // 模式
  mode: 'development', // 开发模式
  // mode: 'production'
}
```

loader: 	1. 下载	2. 使用配置loader

plugins： 	1. 下载 	2. 引入	3. 使用

样式文件处理：

​	loader文件都要下载

​	css文件配置

```JavaScript
{
        // 匹配哪些文件
        test: /\.css$/,
        // 使用哪些loader进行处理
        use: [
          // use数组中loader执行顺序：从右到左，从下到上 依次执行
          // 创建style标签，将js中的样式资源插入进行，添加到head中生效
          'style-loader',
          // 将css文件变成commonjs模块加载js中，里面内容是样式字符串
          'css-loader'
        ]
      }
```

​	less文件配置

```JavaScript
{
        // 匹配哪些文件
        test: /\.css$/,
        // 使用哪些loader进行处理
        use: [
          // use数组中loader执行顺序：从右到左，从下到上 依次执行
          // 创建style标签，将js中的样式资源插入进行，添加到head中生效
          'style-loader',
          // 将css文件变成commonjs模块加载js中，里面内容是样式字符串
          'css-loader',
          'less-loader'
        ]
      }
```

html文件处理：

	1. 下载	npm install html-webpack-plugin -D
 	2. 引入 

```JavaScript
const HtmlWebpackPlugin = require('html-webpack-plugin');
HtmlWebpackPlugin是一个类
```

3.  使用  默认会创建一个空的html，自动引入打包输出的所有资源(JS/CSS)

```
 new HtmlWebpackPlugin({
 		里面的参数复制./src/index.html文件，自动引入打包输出的所有资源(JS/CSS)
        template: './src/index.html'
    })
```

处理图片资源

​	url-loader file-loader url-loader依赖于file-loader

```javascript
npm install --save-dev url-loader file-loader
{
        // 问题：默认处理不了html中img图片
        // 处理图片资源
        test: /\.(jpg|png|gif)$/,
        // 使用一个loader
        // 下载 url-loader file-loader
        loader: 'url-loader',
        options: {
          // 图片大小小于8kb，就会被base64处理
          // 优点: 减少请求数量（减轻服务器压力）
          // 缺点：图片体积会更大（文件请求速度更慢）
          limit: 8 * 1024,
          // 问题：因为url-loader默认使用es6模块化解析，而html-loader引入图片是commonjs
          // 解析时会出问题：[object Module]
          // 解决：关闭url-loader的es6模块化，使用commonjs解析
          esModule: false,
          // 给图片进行重命名
          // [hash:10]取图片的hash的前10位
          // [ext]取文件原来扩展名
          name: '[hash:10].[ext]',
     	  // 指定输出路径
          outputPath: '路径'
        }
      },
      {
        test: /\.html$/,
        // 处理html文件的img图片（负责引入img，从而能被url-loader进行处理）
        loader: 'html-loader'
      }
```

将ES6的语法转化成ES5的语法

```JavaScript
npm install --save-dev babel-loader @babel/core

module: {
  rules: [
    { test: /\.js$/, exclude: /node_modules/, loader: "babel-loader" }
  ]
}
```

vue处理报错信息

```JavaScript
resolve: {
    alias: {
      'vue$': 'vue/dist/vue.esm.js',
    },
  },
```

webpack打包vue文件要使用的loader

```
npm install vue-loader vue-template-compiler --save-dev
```

import时省略后缀名

```JavaScript
resolve: {
    extensions: ['.js', '.css', '.vue'],
  },
```

生成html文件  html-webpack-plugin插件

```javascript
npm install html-webpack-plugin --save-dev
const htmlWebpackPlugin = require('html-webpack-plugin')
new htmlWebpackPlugin({
	template: './index.html' // 指定模板
})
```

webpack-dev-server服务器搭建

```javascript
npm install webpack-cli webpack-dev-server --save-dev  // 必须要有webpack-cli
// 配置
devServer: {
    contentBase: resolve(__dirname, 'dist'),
    compress: true,
    open: true,
  },
```

