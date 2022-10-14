## 开发风格

- 新项目统一使用 vite 作为构建工具
- 组件 script 部分统一使用 "script setup"语法
- 组件代码过多时（例如上千行）且部分模块之间并无逻辑关联，需进行拆分
- 组件 style 模块无特殊情况需添加 scoped 进行样式隔离
- 灵活使用 v-for 减少 dom 重复代码
- 保持 template 模块简洁，可使用计算属性或者方法来得出结果再放到 template 上
- 业务相关公共方法不要和 utils 放在一起，可新建 biz 文件夹
- 公共方法尽量不要挂载到 Vue 类的 prototype 上

## 组件命名

- 命名组件应遵循 PascalCase 约定，也就是组件名应该始终是多个单词的(根组件 App 除外)，并且单词首字母应该大写

```js
// good
export default {
 name: 'TodoItem',
 // ...
}

// bad
export default {
 name: 'Todo',
 // ...
}

```

- 使用组件应遵循 kebab-case 约定，也就是在页面中使用组件，需要前后闭合，并以短线分割。

```html
<div id="app">
  <todo-item></todo-item>
</div>
```

## 目录结构

```js
|— node_modules             项目依赖模块
|— src                      项目源码目录
    |— config               项目配置
        |— dev.env.js       开发环境变量
        |— index.js         主配置文件
        |— prod.env.js      生产环境变量
    |— assets               资源目录，资源会被webpack构建
        |— js               公共js文件目录
        |— css              公共样式文件目录
        |— images           图片存放目录
    |— server               项目部署文件
        |— http.js          axios封装
        |— api.js           接口文件夹
    |— components           项目开发的vue组件
    |— utils                全局方法
    |— hooks                全局hook
    |— routers              前端路由目录
    |— store                vuex(pinia)目录，定义项目状态管理
        |— store.js         组装模块并导出，统一管理导出，也可命名为index.js
    |— App.vue              vue项目的根组件
    |— main.js              入口js文件
|— static                   纯静态资源
|— theme                    element-ui样式库
|— .babelrc                 babel的配置文件
|— .editorconfig            编辑器的配置文件
|— .gitignore               git的忽略配置文件
|— .postcssrc.js            postcss的配置文件
|— isIe.js                  判别浏览器的js文件
|— index.html               html模板，项目入口页面
|— package-lock.json        项目实际安装  的各个npm package的具体来源和版本号
|— package.json             npm包配置文件，依赖包信息
|— README.md                项目介绍
```

局部组件或者局部 hooks 等，不要放在全局组件文件夹中，应放到当前引用页面的文件夹中，以下划线开头例：

```
|— views                           页面
    |— userInfo                    用户信息页面文件夹
        |— _components             用户信息局部组件
           |— userInfoHeader.vue   用户信息头部
        |— _hooks                  用户信息局部hooks
           |— useGetUserInfo.vue   用户信息头部
        |— index.vue               用户信息页面（内部会使用userInfoHeader组件）
```

## 元素属性特性

- 元素特性的顺序，原生属性放前边，指令放后边

```
 - class
  - id,ref
  - name
  - data-*
  - src, for, type, href,value,max-length,max,min,pattern
  - title, alt，placeholder
  - aria-*, role
  - required,readonly,disabled
  - is
  - v-for
  - key
  - v-if
  - v-else-if
  - v-else
  - v-show
  - v-cloak
  - v-pre
  - v-once
  - v-model
  - v-bind,:
  - v-on,@
  - v-html
  - v-text
```
