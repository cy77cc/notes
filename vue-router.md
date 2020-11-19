# vue-router

```javascript
import Vue from 'vue'
import VueRouter from 'vue-router'
// import Home from '../components/Home'
// import About from '../components/About'
// import User from '../components/User'

// 懒加载路由
const Home = () => import("../components/Home")
const About = () => import("../components/About")
const User = () => import("../components/User")

// 1. 通过Vue.use() 安装插件
Vue.use(VueRouter)

// 2. 创建路由对象
const routes = [
  {
    path: '',
    redirect: '/home'
  },
  {
    path: '/home',
    name: 'home',
    component: Home
  }, 
  {
    path: '/about',
    name: 'about',
    component: About
  },
  {
    path: '/user/:userid',
    name: 'user',
    component: User
  }
]

const router = new VueRouter({
  // 配置路由和组件之间的映射关系
  routes,
  // 设置模式
  mode: 'history',
  linkActiveClass: 'active'
})

// 3. 将router对象传入到Vue实例

export default router

/*
  使用vue-router的步骤
  1. 创建路由组件
  2. 配置路由映射，组件和路径映射关系
  3. 使用路由：通过<router-link></router-link> 和 <router-view></router-view>
*/ 
```

App.vue

```vue
<template>
  <div id="app">
    <h2>App组件</h2>
    <!-- tag 指定 router-link组件被解析成什么标签，默认是a标签-->
    <!-- replace不会留下history记录，所以指定replace的情况下，后退键返回不能回到上一个页面 -->
    <!-- active-class 修改默认的激活class名 -->
    <!-- <router-link to="/home" tag="button" replace >首页</router-link>
    <router-lin4k to="/about" tag="button" replace >关于</router-lin4k>
    <button @click="homeClick">首页</button>
    <button @click="aboutClick">关于</button> -->
    <router-link to="/home" replace tag="button">首页</router-link>
    <router-link to="/about" replace tag="button">关于</router-link>
    <router-link :to="'/user/' + userId" replace tag="button">用户</router-link>
    <router-view></router-view>
  </div>
</template>
<script>
export default {
  name: "App",
  data() {
    return {
      userId: "zhangsan",
    };
  },
  methods: {
    // homeClick() {
    //   this.$router.replace("/home");
    // },
    // aboutClick() {
    //   this.$router.replace("/about");
    // },
  },
};
</script>
<style>
button {
  margin: 10px;
}

.active {
  color: red;
}
</style>
```

动态路由



