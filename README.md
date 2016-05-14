# vue-note-firebase-app
一个基于vue.js和Firebase制作的笔记spa（PC端）.

使用vue.js组件开发模式，将spa分为5个component进行开发，基本使用到了vue.js事件通信、过滤器等功能，同时使用Firebase作为后台数据存储端，实现了跨平台数据同步。

目前该spa已经可以实现标签分类、标签\笔记删除、添加以及编辑等基本功能。

本项目有mobile端版本，请移步[vue-vueRouter-note-Firebase-mobile](https://github.com/Geocld/vue-vueRouter-note-Firebase-mobile)

在线[demo](http://geocld.github.io/demo/pc-note/index.html)

#技术栈

框架：[vue.js](http://cn.vuejs.org/)

后台数据同步：[Firebse](https://www.firebase.com/)

UI库：[Semantic UI](http://www.semantic-ui.cn/)

#项目安装
1、安装项目依赖

	npm install

2、发开模式下运行项目

	npm run dev

3、项目正式文件发布

	npm run build

#效果预览
![](http://i.imgur.com/I2KkSfi.png)

#TODO
<del>增加笔记根据日历排序功能</del>

登陆认证功能