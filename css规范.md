# CSS 代码规范指南

## 代码风格

### 代码格式化

样式书写一般有两种：一种是紧凑格式 (Compact)

```ssh
.web{ display: block;width: 50px;}
```

一种是展开格式（Expanded）

```css
.web {
  display: block;
  width: 50px;
}
```

**团队约定:** 统一使用展开格式书写样式

### 代码大小写

样式选择器，属性名，属性值关键字全部使用小写字母书写，属性字符串允许使用大小写。

```css
/* 推荐 */
.web {
  display: block;
}

/* 不推荐 */
.web {
  display: BLOCK;
}
```

### 选择器

- 尽量少用通用选择器 \*
- 不使用 ID 选择器
- 不使用无具体语义定义的标签选择器

```css
/* 推荐 */
.web {
}
.web li {
}
.web li p {
}

/* 不推荐 */
* {
}
#jdc {
}
.web div {
}
```

### 分号

每个属性声明末尾都要加分号；

```css
.web {
  width: 100%;
  height: 100%;
}
```

### 代码易读性

颜色值 rgb() rgba() hsl() hsla() rect() 中不需有空格，且取值不要带有不必要的 0

```css
/* 推荐 */
.web {
  color: rgba(255, 255, 255, 0.5);
}

/* 不推荐 */
.web {
  color: rgba(255, 255, 255, 0.5);
}
```

不要为 0 指明单位

```css
/* 推荐 */
.web {
  margin: 0 10px;
}

/* 不推荐 */
.web {
  margin: 0px 10px;
}
```

### CSS3 浏览器私有前缀写法

CSS3 浏览器私有前缀在前，标准前缀在后

```css
.web {
  -webkit-border-radius: 10px;
  -moz-border-radius: 10px;
  -o-border-radius: 10px;
  -ms-border-radius: 10px;
  border-radius: 10px;
}
```

### class 命名

- 避免过度任意的简写。.btn 代表 button，但是 .s 不能表达任何意思。
- class 名称应当尽可能短，并且意义明确。
- 随着项目模块增多，防止因为不同页面或者组件中定义的 css 冲突，所以规范 css 语法也变得至关重要，推荐:BEM，分别代表着:Block(块)、Element(元素)、Modifier(修饰符)

```ssh
.user-info {} # user-info 是一个块，我理解是一个模块
.user-info--feature {} # user-info--feature 是一个修饰符，用来表示这个块的不同状态
.user-info__title{} # user-info__title 是一个元素，属于userinfo模块下的，多个元素组成块
```

```html
<div class="user-info">
  <div class="user-info__title">张三</div>
  <div class="user-info__age">18</div>
</div>

<div class="tabs">
  <div class="tab tab-active">选中的标签</div>
  <div class="tab ">标签二</div>
  <div class="tab ">标签三</div>
</div>
```

### css 属性声明顺序

1. Positioning
2. Box model
3. Typographic
4. Visual
5. Misc

由于定位（positioning）可以从正常的文档流中移除元素，并且还能覆盖盒模型（box model）相关的样式，因此排在首位。盒模型排在第二位，因为它决定了组件的尺寸和位置。

其他属性只是影响组件的 内部 或者是不影响前两组属性，因此排在后面。

```css
.declaration-order {
  /* Positioning  定位和层级等属性*/
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 100;

  /* Box-model 盒子模型或者浮动相关*/
  display: block;
  float: right;
  width: 100px;
  height: 100px;

  /* Typography 字体配置*/
  font: normal 13px "Helvetica Neue", sans-serif;
  line-height: 1.5;
  color: #333;
  text-align: center;

  /* Visual 背景色边框等*/
  background-color: #f5f5f5;
  border: 1px solid #e5e5e5;
  border-radius: 3px;

  /* Misc 透明度和动画等*/
  opacity: 1;
  transition: all 0.5s;
}
```

## SCSS 规范

我们开发将使用 SCSS 来作为 css 的预处理器

### 变量

可复用属性尽量抽离为页面变量，易于统一维护

```scss
// CSS
.web {
  color: red;
  border-color: red;
}

// SCSS
$color: red;
.web {
  color: $color;
  border-color: $color;
}
```

### 混合(mixin)

根据功能定义模块，然后在需要使用的地方通过 @include 调用，避免编码时重复输入代码段

```scss
// CSS
.web_1 {
  -webkit-border-radius: 5px;
  border-radius: 5px;
}
.web_2 {
  -webkit-border-radius: 10px;
  border-radius: 10px;
}

// SCSS
@mixin radius($radius: 5px) {
  -webkit-border-radius: $radius;
  border-radius: $radius;
}
.web_1 {
  @include radius; //参数使用默认值
}
.web_2 {
  @include radius(10px);
}

// CSS
.web_1 {
  background: url(/img/icon.png) no-repeat -10px 0;
}
.web_2 {
  background: url(/img/icon.png) no-repeat -20px 0;
}

// SCSS
@mixin icon($x: 0, $y: 0) {
  background: url(/img/icon.png) no-repeat $x, $y;
}
.web_1 {
  @include icon(-10px, 0);
}
.web_2 {
  @include icon(-20px, 0);
}
```

### function 函数

```scss
@function pxToRem($px) {
  @return $px / 10px * 1rem;
}
.web {
  font-size: pxToRem(12px);
}
```

### 运算规范

运算符之间空出一个空格

```scss
.web {
  width: 100px - 50px;
  height: 30px / 5;
}
```

注意运算单位，单位同时参与运算，所以 10px 不等于 10，乘除运算时需要特别注意

```scss
// 正确的运算格式
.web {
  width: 100px - 50px;
  width: 100px + 50px;
  width: 100px * 2;
  width: 100px / 2;
}
```
