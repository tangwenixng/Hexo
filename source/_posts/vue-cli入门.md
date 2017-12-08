---
title: vue-cli入门
date: 2017-11-18 12:13:40
tags: [vue]
categories: 教程
---

## 安装vue-cli

`npm install -g vue-cli` 全局安装vue-cli

(注：npm会有点慢，建议更改为国内淘宝的镜像，只换源即可。在cmd输入命令：npm config set registry https://registry.npm.taobao.org)

---

## 构建vue-cli项目

`vue init webpack projectname` 

---

## 安装依赖
`npm install`

---
## 运行项目

`npm run dev`
打开 http://localhost:8080 访问

---

## vue-cli项目结构

![总体结构](http://upload-images.jianshu.io/upload_images/5700710-cebf33ac17019737.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

1. build
主要启动文件是dev-server.js，当我们输入npm run dev首先启动的就是dev-server.js

2. config
![config](http://upload-images.jianshu.io/upload_images/5700710-81ac9bc6b912d0fc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3. src 源码
    -  **index.html(主页)**
    index.html如其他html一样，但一般只定义一个空的根节点，在main.js里面定义的实例将挂载在根节点下，内容都通过vue组件来填充

    - **App.vue**
    一个vue页面通常由三部分组成:模板(template)、js(script)、样式(style)
    ![](http://upload-images.jianshu.io/upload_images/5700710-6b6087ca3510a257.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

    【template】

    **其中模板只能包含一个父节点，也就是说顶层的div只能有一个**（例如下图，父节点为#app的div，其没有兄弟节点）

    <router-view></router-view>是子路由视图，后面的路由页面都显示在此处

    打一个比喻吧,<router-view>类似于一个插槽，跳转某个路由时，该路由下的页面就插在这个插槽中渲染显示

    【script】

    vue通常用es6来写，用export default导出，其下面可以包含数据data，生命周期(mounted等)，方法(methods)等，具体语法请看vue.js文档

    - **main.js 入口文件**
    main.js主要是引入vue框架，根组件及路由设置，并且定义vue实例

    - **router——[路由配置]**
    router文件夹下，有一个index.js，即为路由配置文件
    ![](http://upload-images.jianshu.io/upload_images/5700710-547eb7db1fbff32f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


## webex-cli
[webex-cli](https://github.com/tangwenixng/webex-cli) 这是我用vue-cli搭建的一个项目，基本功能都覆盖了，放在github上。


[参考--vue-cli入门（二）——项目结构](http://www.jianshu.com/p/7006a663fb9f)


