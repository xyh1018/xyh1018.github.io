---
layout: post
title: Vue-router
date: 2022-12-11 04:16
author: "xyh"
tags:
    - Vue
    - Vue-router
---
## 动态路由
#### 如何传值给路由页面
1. `<router-link to="/path?参数名=值"></router-link>`
2. `path: '/path/:参数名'` | `<router-link to="/path/值"></router-link>`
#### 如何接受路由传值
1. `$route.query.参数名`
2. `$route.params.参数名`

## 路由重定向
```js
{
  path: '/',
  name: 'roott',
  redirect: './two'
}
```
使用 `redirect` 配置项，值是要切换的路由路径

## 路由404设置
1. 创建一个404的组件
2. 在router里配置它，把404组件添加到routes数组的最后一项
3. 当路由找不到有效路径时就会启用404组件

## 路由模式修改
- hash路由：http://localhost:8080/#/home
- history路由：http://localhost:8080/home (以后上线需要服务器端支持，否则找的是文件夹)
```js
const router = createRouter({
  history: createWebHistory(),
  routes
})
```
在v4版本中，如果希望使用hash路由，在创建router时在history配置项中使用`createWebHashHistory()`。如果希望使用history路由，使用`createWebHistory()`

## 编程式导航
---
    声明式: <router-link :to="...">
    编程式: router.push(...)
---
### 跳转路由
想要导航到不同的 URL，可以使用 `router.push` 方法。这个方法会向 history 栈添加一个新的记录，所以，当用户点击浏览器后退按钮时，会回到之前的 URL。当你点击 \<router-link> 时，内部会调用这个方法，所以点击 \<router-link :to="..."> 相当于调用 router.push(...)
```js
// 路由路径切换
this.$router.push({path})
// 路由名切换
this.$router.push({ name: 'user'})
```
该方法的参数可以是一个字符串路径，或者一个描述地址的对象
### 传参
1. 使用`path`
```js
router.push({ 
    path: '/register', query: { plan: 'private' } 
})
```
2. 使用`name`
```js
router.push({ 
    name: 'user', params: { username: 'eduardo' } 
})
router.push({ 
    name: 'user', query: { username: 'eduardo' } 
})
```
注意：`path` 不能和 `params`一起使用

推荐使用 name + params 的方式来跳转路由和传参
