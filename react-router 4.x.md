**react-router 4.x**

1、npm install react-router-dom --save

2、import { BrowserRouter as Router, Route, Link } from "react-router-dom"

3、根组件里面引用设置

4、exact表示严格匹配

```JavaScript
function App() {
  return (
    <Router>
        <div>
        <ul>
                <li>
                    <Link to="/">home</Link>
                </li>
                <li>
                    <Link to="/news">news</Link>
                </li>
                <li>
                    <Link to="/list">list</Link>
                </li>
            </ul>
            <hr/>
            <Route exact path="/" component={Home} />
            <Route path="/news" component={News} />
            <Route path="/list" component={List} />
            <Route path="/content/:aid" component={component} />
        </div>
    </Router>
  );
}
```

react-router可以让根组件动态的去挂载不同的组件，根据用户访问的地址动态的加载不同的组件

**动态路由设置**

url存储在props里面的match里面 

path  访问的路径

url 网页访问的url 

:aid 对应的是url里面的1

挂载的时候设置

```javascript
match: {
    path: "/content/:aid", 
    url: "/content/1", 
    isExact: true, 
    params: {…}
}

<Link to={`/content/${value.aid}`}>{value.title}</Link>
```

get传值 

get传值传递的url数据存储在location里面  可以用url模块处理传递的url

npm install url --sava

```javascript
location: {
    pathname: "/productcontent", 
    search: "?aid=2", 
    hash: "", 
    state: undefined, 
    key: "zbfi0g"
}
```

**JavaScript实现路由跳转**

1、引入 

```
import { Redirect } from "react-router-dom";
```

1、定义loginFlag判断跳转 true跳转 false不跳转

```javascript
if(this.state.loginFlag){   
    return <Redirect to={{pathname: "/"}} /> 
    path是满足条件之后跳转的url页面 
}
```

**路由嵌套**

把链接的组件放在一个盒子中

当点击用户中心的时候在右边盒子加载Main组件 点击用户信息的时候在右边盒子加载Info组件

```javascript
当点击用户中心的时候在右边盒子加载Main组件
点击用户信息的时候在右边盒子加载Info组件
<div className="left">
    <Link to="/user/">用户中心</Link>
    <Link to="/user/info">用户信息</Link>
</div>
<div className="right>
    <Route exact path="/user/" component={Main} />
    <Route exact path="/user/info" component={Info} />
</div>
```

**路由模块化**

把路由放在单独的文件中

```javascript
封装到项目的model下面的routes.js中
var routes = [
    {
        path: "/",   路径
        component: "Home",   加载的组件
        exact: true   严格匹配
    },{
        path: "/shop",   路径
        component: "Shop",   加载的组件
        exact: false,
        routes: [
            {
                path:"/shop/",
                component: "ShopHome",
                exact: true
            },{
                path: "/shop/list",
                component: "ShopList",
                exact: false
            }
        ]
    },{
        path: "/user",   路径
        component: "User",   加载的组件
        exact: false
    }
]
遍历添加路由
routes.map((value, key) => {
    if(value.exact) {
        return <Route exact path={value.path} component={value.component} key={key} />
    } else {
        return <Route path={value.path} component={value.component} key={key} />
    }
})
```

通过render传递

```javascript
<Route exact path="shop" render={(props) => {    
	return <ShopHome {...props} routes={传递的路由参数} /> 
}}
```

