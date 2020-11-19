# Nodejs

## 1 入门

创建一个简单的服务

```js
// 1. 首先引入http模块
const http = require('http')

// 2. createServer 会创建新的http服务器，并返回
const app = http.createServer((req, res) => {
  res.statusCode = 200
  res.setHeader = ('Content-Type', 'text/html')
  res.end('<h1>Hello, World</h1>')
}) 

app.listen(3000, () => {
  console.log('服务启动成功')
})
```

## 2 process

process.env 方法可以访问系统的环境变量

process.argv 可以接受命令参数

## 3 chalk

chalk包可以改变命令行输出的颜色

```js
const chalk = require('chalk')
console.log(chalk.blue('你好'))
```

## 4 progress

progress 可以用于创建进度条

```js
const Progress = require('progress')
const bar = new Progress(':bar', {total: 10})
const timer = setInterval(() => {
  bar.tick()
  if (bar.complete) {
    clearInterval(timer)
  }
}, 100)
```

