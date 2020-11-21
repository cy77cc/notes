```js
const fs = require('fs')
创建目录
fs.mkdir('11', err => {
  if (err) throw err
  else console.log('创建成功')
})

// 修改目录名称
fs.rename('11', '22', err => {
  if (err) throw err
  else console.log('修改成功')
})

// 读取目录
fs.readdir('node_modules', (err, data) => {
  if (err) throw err
  else console.log(data)
})

// 删除目录 (一定要是一个空目录)  加上  recursive 递归删除
fs.rmdir('22', { recursive: true }, err => {
  if (err) throw err
  else console.log('删除成功')
})

// 判断文件或目录是否存在
fs.access('home', (err) => {
  if (err) {
    console.log('目录或文件不存在')
  }
  else {
    console.log('目录或文件存在')
  }
})

// 获取文件或者目录的详细信息
fs.stat("index.js", (err, stats) => {
  if (err) {
    return console.log(err)
  } else {
    console.log(stats.isDirectory())
    console.log(stats)
  }
})
```

同样的fs目录操作加上Sync就变成同步的