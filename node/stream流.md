```js
const fs = require('fs')

let buffer = Buffer.alloc(65 * 1024)
fs.writeFile('65kb.txt', buffer, err => {
  if (err) return console.log(err)
  else console.log('写入成功')
})

// 流会把数据分成64kb的小文件传输
let rs = fs.createReadStream('./65kb.txt')
let str = ''
// rs.on 监听事件
rs.on("data", chunk => {
  console.log(chunk)
  str += chunk
})
// 流完成了
rs.on("end", () => {
  console.log(str)
})

let rs = fs.createReadStream("package-lock.json")
let ws = fs.createWriteStream("2.txt")
// pipe管道
rs.pipe(ws)
```

