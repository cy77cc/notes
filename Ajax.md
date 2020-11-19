# Ajax

```js
// 1. 创建对象
const xhr = new XMLHttpRequest()
// 2. 初始化 设置请求方式和 url
xhr.open('GET', 'http://localhost:8000/server?name=张三')
// 3. 发送请求
xhr.send()
// console.log(xhr)
xhr.onreadystatechange = function() {
    // console.log('123')
    // readystate 是xhr对象中的属性，表示状态 0 1 2 3 4 五个值
    // 状态为4的时候服务端返回了所有的结果
    if(xhr.readyState === 4) {
        // console.log(xhr.status)
        if(xhr.status >= 200 && xhr.status < 300) {
            // console.log(xhr.status) // 相应状态码
            // console.log(xhr.statusText) // 状态字符串
            // console.log(xhr.getAllResponseHeaders) // 
            // console.log(xhr.response) // 响应体
            console.log(xhr.responseURL)
            result.innerHTML = xhr.response
        }
    }
}

处理POST请求
const xhr = new XMLHttpRequest()
xhr.open('POST', 'http://localhost:8000/server')
// 设置请求头
xhr.setRequestHeader('Content-Type', 'application/x-www.form-urlencoded')
xhr.send('a=100&b=200')
xhr.onreadystatechange = function() {
    if (xhr.readyState === 4) {
        // console.log('1')
        if (xhr.status >= 200 && xhr.status < 300) {
            // console.log(xhr)
            result.innerHTML = xhr.response
        }
    }
}
json格式处理
const xhr = new XMLHttpRequest()
// 设置响应体数据类型
xhr.responseType = 'json'
xhr.open('GET', 'http://localhost:8000/json-server')
xhr.send()
xhr.onreadystatechange = function () {
    if (xhr.readyState === 4) {
        if (xhr.status >= 200 && xhr.status < 300) {
            // let data = JSON.parse(xhr.response)
            // result.innerHTML = data.name
            // console.log(data)
            console.log(xhr.response)
            result.innerHTML = xhr.response.name
        }
    }
}

ie缓存问题
ie在请求相同的url时会有缓存问题
const xhr = new XMLHttpRequest()
// Date.now() 获取当前时间戳所以每次请求都不一样
xhr.open('get', 'http://localhost:8000/ie?t=' + Date.now())
// 设置请求头
xhr.onreadystatechange = function() {
    if (xhr.readyState === 4) {
        // console.log('1')
        if (xhr.status >= 200 && xhr.status < 300) {
            // console.log(xhr)
            result.innerHTML = xhr.response
        }
    }
}
```

