# redux

yum -y install redux --save

创建store文件夹里面有index.js和reducer.js文件

todolist.js

```javascript
import React from "react"
import 'antd/dist/antd.css'
import { Input, Button, List } from 'antd'
import store from '../store/index'

export default class Todolsit extends React.Component {
    constructor(props) {
        super(props)
        this.state = store.getState()
        store.subscribe(this.storeChange) // 订阅redux的状态
    }

    changeInputValue = (e) => {
        const action = { // 创建action
            type: 'changeInput',
            value: e.target.value
        }
        store.dispatch(action) // 传递action给reducer里面
    }

    storeChange = () => {
        this.setState(store.getState)
    }

    render() {
        return (
            <div style={{ margin: '10px' }}>
                <div>
                    <Input placeholder={this.state.inputValue} 
                        style={{ width: '250px', marginRight: '10px' }} 
                        onChange={this.changeInputValue}
                    />
                    <Button type="primary" >提交</Button>
                </div>
                <div style={{ margin: '10px', width: '300px' }}>
                    <List
                        // borderd={true}
                        dataSource={this.state.list}
                        renderItem={item=>(<List.Item>{item}</List.Item>)}
                    />
                </div>
            </div >
        )
    }
}
```

index.js

```JavaScript
import { createStore } from 'redux' // 引入createStore方法
import reducer from './reducer'
const store = createStore(reducer) // 创建数据存储仓库
window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__() // 插件调试
export default store // 暴露出去
```

reudcer.js

```JavaScript
const defaultState = {
    inputValue: 'Write Someting',
    list: [
        "早8点开晨会，分配今天的开发工作",
        "早9点和项目经理作开发需求讨论会",
        "晚5:30对今日代码进行review",
    ]
}

export default (state = defaultState, action) => { // 就是一个方法函数
    if (action.type === 'changeInput') {
        let newState = JSON.parse(JSON.stringify(state)) // 深度拷贝state
        newState.inputValue = action.value
        return newState
    }
    return state
}
```

reducer.js是存储管理数据的文件，index.js暴露数据

在文件中引入store下面的index.js调用store对象下面的getState方法就可以获取数据

store下面的方法

```
dispatch: ƒ dispatch(action)
getState: ƒ getState()
replaceReducer: ƒ replaceReducer(nextReducer)
subscribe: ƒ subscribe(listener)
Symbol(observable): ƒ observable()
```











