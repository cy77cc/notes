# HTTP

## 入门案例

```js
const http = require('http')
res  相应对象
req  请求对象
const server = http.createServer()
app.on 监听事件
server.on('requese', (req, res) => {
    res.setHeader('Content-Type', 'text/html;charset=utf-8')
	res.end('Hello, World')
})
server.listen(3000)
```

## response对象

* res.setHeader   设置头信息

    ```js
    res.setHeader('Content-Type', 'text/html;charset=utf-8')
    ```

* res.end(相应内容)

    ```
    // 文件方式
    fs.readFile('./views/index.html', (err, data) => {
    	if (err) {
    		throw err
    	} else {
    		res.end(data)
    	}
    })
    // 流方式
    let fileData = fs.createReadStream('./views/index.html')
    fileData.pipe(res)
    ```

    

## request对象

* req.url   获取页面请求的url

## url处理url

url模块用于解析url

const { URL } = require('url')   结构新的解析url的方式

* new URL(input[, base])   如果input不是绝对路径就要添加base

    ```js
    const myurl = new URL(req.url, 'http://localhost:3000/')
    ```

    ```js
    href: 'http://localhost:3000/favicon.ico',   	路径
    origin: 'http://localhost:3000',				base地址
    protocol: 'http:',								协议
    username: '',									用户名
    password: '',									密码
    host: 'localhost:3000',							主机
    hostname: 'localhost',							主机名
    port: '3000',									端口
    pathname: '/favicon.ico',						请求路径
    search: '',										?后面的参数
    searchParams: URLSearchParams {},				搜索参数
    hash: ''										hash哈希
    ```

* 