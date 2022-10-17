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
