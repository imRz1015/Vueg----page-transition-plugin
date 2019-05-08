2019-05-08

<h3>这个分支主要是为了解决该插件在IOS8.X的版本中不兼容，可能造成项目白屏的问题</h3>
<p>主要问题在于ES6中，Object.assign()不能被babel转为ES5（也有可能是我配置错了的原因..emmmmmmmm）</p>
<p>这个分支仅仅将Object.assign()这个方法做了兼容处理，采用for in 的方式去遍历合并对象</p>
<p>如果你的babel-polyfill可以正常转码，那么你可以直接使用作者的master分支</p>

<h4>PS:为了方便我还顺便把它抽出来放进了dist文件夹，因为这个分支就算你看到了你也不能通过npm下载，除非作者哪天看到了墙角瑟瑟发抖的我并好心解决了这个问题....如果不行，请先npm i animate.css --save ，然后直接把dist放进你的项目中，然后import vueg from './dist/index.js'就可以了，剩下的就按照作者文档正常使用就OK</h4>


[![](https://raw.githubusercontent.com/jaweii/vueg/master/image/vueg.JPG "LOGO")](https://raw.githubusercontent.com/jaweii/vueg/master/image/vueg.JPG)


<p align="center">
    <a href="https://github.com/996icu/996.ICU/blob/master/LICENSE">
        <img alt="996icu" src="https://img.shields.io/badge/license-NPL%20(The%20996%20Prohibited%20License)-blue.svg">
    </a>
</p>
<br>


## Example：

<img src="https://raw.githubusercontent.com/jaweii/Vueg----page-transition-plugin/master/image/GIF.gif" height="600"/>


## 使用方法

#### 安装插件

```js
npm i vueg --save
```

#### 引入插件
```js
import vueg from 'vueg'

Vue.use(vueg, new Router(), Options) // 传入实例化后的router, Options为可选的插件配置

```
#### 插件指令
插件注册了名为`v-transition`的指令，接收一个可选的Options参数，其包含的配置优先级高于全局配置。

#### 启用插件：

为`router-view`添加`v-transition`指令后，该`router-view`下所有的页面都将启用动画：
```js
<router-view v-transition></router-view>
```
或，为`template`中的顶级标签添加`v-transition`指令后，该页面组件将启用动画效果:
```js
<template>
    <page v-transition>
    </page>
</template>
```

支持Nuxt。


---

## Options

```js
@property {number} duration 动画时长。默认为0.3
@property {string} enter 入场动画，默认为'fadeInRight'
@property {string} leave 离场动画，默认为'fadeInLeft'
@property {boolean} disableAtSameDepths 深度相同时禁用动画(通过url中的反斜杠数量/判断)。默认为false
@property {boolean} shadow 是否为入场页面添加阴影。默认为true
@property {Object} map 默认为空情况下，vueg根据url深度判断是入场还是离场，但有时可能并不是你想要的效果，这时你可以使用map选项。
例子：`
map: {
 'user-login':{
    enter: ['user-register'],
    leave: ['index'],
    disable: ['user-login-sms']
  }
 }
 `
上面例子表示，从名为`user-login`的路由到名为`user-regiseter`的路由转场，使用入场动画，反之则使用离场动画。
从名为`user-login`的路由到名为`index`的路由转场，使用离场动画，反之则使用入场动画。
从名为`user-login`的路由到名为`user-login-sms`的路由转场，禁用转场动画。



```

`enter`、`leave` 参数使用的animate.css的动画类名作为值，查看全部可用值，请访问：[https://daneden.github.io/animate.css](https://daneden.github.io/animate.css)。
另外插件自带了一个可用值 `touchPoint`，动画效果为页面从触摸(点击)点放大入场。

