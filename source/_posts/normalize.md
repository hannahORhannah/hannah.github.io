---
title: vue 项目工程化规范
date: 2020-02-26 23:50:10
tags: vue
---
## 文件命名规范

> folder：文件夹命名采用中划线连接
> 反例：serviceCustomer ServiceCustomer Users uiComponents
> 推荐：service-customer users

> .js：一般的js文件采用小驼峰的命名方式。如果是类文件，则使用大驼峰的命名方式
> 反例：service-customer.js
> 推荐：serviceCustomer.js ServiceCustomer.js(仅限类文件)

> .vue：官方推荐使用大驼峰或者中划线的方式命名。[单文件组件官方命名规范](https://cn.vuejs.org/v2/style-guide/#单文件组件文件的大小写-强烈推荐)
> 反例：myComponent.vue
> 可使用：MyComponent.vue
> 推荐：my-component.vue

引入vue组件的时候需要转换为大驼峰 推荐：`import MyComponent from '@/components/my-component'`
 以上命名规范是在参考`iview`，`iview-admin`，`element`等一些vue开源项目并结合vue官方文档以及当前的开发习惯得出的推荐用法。
 更多vue的风格指南请参考[官方风格指南](https://cn.vuejs.org/v2/style-guide/)

## 目录结构

此目录为src文件下的目录结构

```
├── api
│   ├── user.js
│   └── news.js
├── assets
│   └── images
├── components
│   └── biz-alert
│       ├── index.js
│       └── biz-alert.vue
│   └── cell-group
│       ├── index.js
│       └── cell-group.vue
├── libs
│   ├── ajax.js
│   └── excel.js
├── mixins
│   ├── news.js
│   └── user.js
├── router
│   └── modules
│       ├── news.js
│       └── users.js
│   └── index.js
├── store
│   └── modules
│       ├── news.js
│       └── users.js
│   └── index.js
├── styles
│   └── common.css
├── utils
│   └── util.js
├── views
│   ├── news
│   └── users
├── App.vue
└── main.js
复制代码
```

### api

api目录用于存放api请求，即所有的api都放在这个目录下进行管理，无特殊情况不要在项目的其他文件夹或文件中出现api路由。文件命名采用类似apiUser.js的命名方式，以便区分是api或者是别的js文件。api目录下对不同模块再进行分类管理，如用户相关的api统一写在apiUser.js中，订单统一写在apiOrder.js中。

采用这种目录及命名的原因：

1. 根据业务模块，对api进行模块划分，方便管理和维护。

2. js命名方式遵循文件命名规范，在此基础上加上前缀api，以便区分api文件。

3. export default apiUser 根据sonar的规范(By convention, a file that exports only one class, function, or constant should be named for that class, function or constant. Anything else may confuse maintainers.)。必须和文件名一样

   ![api file pic](https://user-gold-cdn.xitu.io/2019/6/21/16b7933c6e8ad417?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

### assets

assets目录主要存放图片文件，图片文件命名没有标准的规范。可参考[图片命名规范](https://guide.aotu.io/docs/name/image.html)

### components

存放公共组件，在一个项目中或多或少的存在一些复用的组件，这一类的组件统一在这个目录下进行管理。
 建议每一个组件用一个单独的目录进行管理，在index.js把组件暴露出去，这种做法方便做一些扩展。带来的问题是，可能需要多创建一个index.js，多写几行代码。
 采用这种目录结构以及引入index.js的方式，主要参考一些开源的后台管理项目。`iview-admin` ，`iview`， `飞冰的ICE Design Pro的模板`。

![componet js pic](https://user-gold-cdn.xitu.io/2019/6/21/16b7937d9759ee1f?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

![compontent vue pic](https://user-gold-cdn.xitu.io/2019/6/21/16b7936d94f2b942?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



### libs

libs目录存放插件封装和配置, 比如 axios,vue-lazy等

![axios pic](https://user-gold-cdn.xitu.io/2019/6/21/16b793a37dec15d8?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



### mixins

mixins目录用来存放各个混入对象

### router

router目录用来存放路由信息和导航守卫。
 大型项目中建议在`router/index.js`管理所有路由相关的内容，包括路由的基本配置信息、导航守卫。路由信息则按照模块来管理，在方便管理路由信息的同时避免某个文件过大（超过800行），这样的组织结构会更加清晰，demo如下。也可参考[vue-element-admin](https://github.com/PanJiaChen/vue-element-admin)
 中型项目可以在一个文件中管理路由信息，在index.js中配置导航守卫。可参考 [iview-admin](https://github.com/iview/iview-admin)
 小项目中可以在router/index.js中管理所有的路由信息及导航守卫。\

优点：

1. 职责明确
2. 结构清晰，易于管理

不推荐：

1. 在main.js中处理导航守卫，带来的问题main.js职责不明确，文件过大
2. 路由文件超过800行（目前的项目中的路由信息，有部分存在或即将存在这个问题）



![router pic](https://user-gold-cdn.xitu.io/2019/6/21/16b793d3f23c4e57?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

![router module pic](https://user-gold-cdn.xitu.io/2019/6/21/16b793db31d514c7?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



### store

store目录主要用于vuex状态管理。

![img](https://user-gold-cdn.xitu.io/2019/6/21/16b793edb9a3062b?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



### styles

styles目录用于存放一些公共的样式文件。

### utils

utils 目录存放辅助函数。

### views

views为业务视图。
 这个目录下的结构组织可根据模块或者页面去组织。

## 总结

遵循上述的规范，能避免我们在开发过程中的一些痒点，优化我们的项目结构。目的是让帮助我们开发人员在各个项目中流动，大大降低学习和熟悉项目的成本。
 这个项目结构的规范主要借鉴了egg的设计思想，并参考了部分开源项目的设计和命名规范。