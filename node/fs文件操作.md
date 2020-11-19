**fs.writeFile(file, data [,option], callback)**  写文件  [文档说明](http://nodejs.cn/api/fs.html#fs_fs_writefile_file_data_options_callback)

```js
new Promise((resolve, reject) => {
  fs.writeFile('1.txt', '我是写入的文字11111\n', (err) => {
    if (err) {
      reject(err)
    } else {
      resolve('写入成功')
    }
  })
}).then(result => {
  console.log(result)
  return new Promise((resolve, reject) => {
    fs.writeFile('1.txt', '我是写入的文字2222', { flag: "a" }, (err) => {
      if (err) {
        reject(err)
      } else {
        resolve('写入成功')
      }
    })
  })
}, err => {
  console.log(err)
})
  .then(result => {
    console.log(result)
  }, err => {
    console.log(err)
  })
```

**fs.readFile(path [, options], callback)  读取文件**  [文档说明](http://nodejs.cn/api/fs.html#fs_fs_readfile_path_options_callback)

```js
fs.readFile('.1.txt', 'utf8', (err, data) => {
  if (err) {
    throw err
  } else {
    console.log(data)
  }
})

fs.readFile('1.txt', (err, data) => {
  if (err) {
    throw err
  } else {
    console.log(data.toString())
  }
})
```

所有文件操作没有加上Sync都是异步 否则是同步

```js
let data = fs.readFileSync('1.txt','utf8')
console.log(data)
```

**fs.rename(oldFileName, newFileName, callback)  重命名文件**  [文档说明](http://nodejs.cn/api/fs.html#fs_fs_rename_oldpath_newpath_callback)

```js
fs.rename('1.txt', '2.txt', err => {
  if (err) throw err
})
```

**fs.unlink(path, callback)  删除文件**  [文档说明](http://nodejs.cn/api/fs.html#fs_fs_unlink_path_callback)

```
fs.unlink('2.txt', err => {
	if (err) throw err
	else console.log('删除成功')
})
```

fs.copyFile(src, dest[, mode], callback) 复制文件  先读取后写入 [文档说明](http://nodejs.cn/api/fs.html#fs_fs_copyfile_src_dest_mode_callback)

```js
fs.copyFile('index.js', 'myindex.js', err => {
  if (err) throw err
  else console.log('复制成功')
})
```

