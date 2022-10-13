## JavaScript 风格指南

### 变量

#### 变量声明

- 标准变量统一使用小驼峰，如 userInfo，activeIndex
- 常量全大写，用下划线连接，如 BASE_URL，DOMAIN
- 构造函数，大写第一个字母
- 变量名需要具有语义化，不要声明 a，bb,div1,xcx 等名称
- 作用域不大临时变量可以简写，比如：str,num,obj,un,arr。
- 禁止使用 let，统一使用 let 或 const

#### 对数据进行声明，避免用意不明的数据

```js
//正例：
const MINUTES_IN_A_YEAR = 525600;
for (let i = 0; i < MINUTES_IN_A_YEAR; i++) {
  runCronJob();
}

//反例：
// 525600 是什么?
for (var i = 0; i < 525600; i++) {
  runCronJob();
}
```

#### 避免重复的描述

```js
//正例：
let Car = {
  make: "Honda",
  model: "Accord",
  color: "Blue",
};

//反例：
let Car = {
  carMake: "Honda",
  carModel: "Accord",
  carColor: "Blue",
};
```

### 函数

#### 函数参数 (理想情况下应不超过 2 个)

限制函数参数数量很有必要，这么做使得在测试函数时更加轻松。过多的参数将导致难以采用有效的测试用例对函数的各个参数进行测试。

应避免三个以上参数的函数。通常情况下，参数超过两个意味着函数功能过于复杂，这时需要重新优化你的函数。当确实需要多个参数时，大多情况下可以考虑这些参数封装成一个对象。

JS 定义对象非常方便，当需要多个参数时，可以使用一个对象进行替代。

```js
//正例：
let menuConfig = {
  title: 'Foo',
  body: 'Bar',
  buttonText: 'Baz',
  cancellable: true
}

function createMenu(menuConfig) {
  ...
}

//反例：
function createMenu(title, body, buttonText, cancellable) {
  ...
}
```

#### 函数命名

- 驼峰式命名，统一使用动词，或者动词+名词形式

```js
//正例：
jumpPage、openUserInfoDialog

//反例：
go、nextPage、show、open、login
```

- 请求数据方法，以 data 结尾

```js
// good
getListData   postFormData

// bad
getList  postForm
```

- 尽量使用常用单词开头

```js
set、get、open、close、jump
```

附：函数方法昂用的动词

```js
get 获取/set 设置,
add 增加/remove 删除
create 创建/destory 移除
start 启动/stop 停止
open 打开/close 关闭,
read 读取/write 写入
load 载入/save 保存,
create 创建/destroy 销毁
begin 开始/end 结束,
backup 备份/restore 恢复
import 导入/export 导出,
split 分割/merge 合并
inject 注入/extract 提取,
attach 附着/detach 脱离
bind 绑定/separate 分离,
view 查看/browse 浏览
edit 编辑/modify 修改,
select 选取/mark 标记
copy 复制/paste 粘贴,
undo 撤销/redo 重做
insert 插入/delete 移除,
add 加入/append 添加
clean 清理/clear 清除,
index 索引/sort 排序
find 查找/search 搜索,
increase 增加/decrease 减少
play 播放/pause 暂停,
launch 启动/run 运行
compile 编译/execute 执行,
debug 调试/trace 跟踪
observe 观察/listen 监听,
build 构建/publish 发布
input 输入/output 输出,
encode 编码/decode 解码
encrypt 加密/decrypt 解密,
compress 压缩/decompress 解压缩
pack 打包/unpack 解包,
parse 解析/emit 生成
connect 连接/disconnect 断开,
send 发送/receive 接收
download 下载/upload 上传,
refresh 刷新/synchronize 同步
update 更新/revert 复原,
lock 锁定/unlock 解锁
check out 签出/check in 签入,
submit 提交/commit 交付
push 推/pull 拉,
expand 展开/collapse 折叠
begin 起始/end 结束,
start 开始/finish 完成
enter 进入/exit 退出,
abort 放弃/quit 离开
obsolete 废弃/depreciate 废旧,
collect 收集/aggregate 聚集
```

#### 采用默认参数精简代码

```js
//正例：
function writeForumComment(subject = 'No subject', body = 'No text') {
  ...
}

//反例：
function writeForumComment(subject, body) {
  subject = subject || 'No Subject';
  body = body || 'No text';
}
```

#### 使用 Object.assign 设置默认对象

```js
//正例：
let menuConfig = {
  title: "Order",
  // User did not include 'body' key
  buttonText: "Send",
  cancellable: true,
};

function createMenu(config) {
  config = Object.assign(
    {
      title: "Foo",
      body: "Bar",
      buttonText: "Baz",
      cancellable: true,
    },
    config,
  );

  // config now equals: {title: "Order", body: "Bar", buttonText: "Send", cancellable: true}
  // ...
}

createMenu(menuConfig);

//反例：
let menuConfig = {
  title: null,
  body: "Bar",
  buttonText: null,
  cancellable: true,
};

function createMenu(config) {
  config.title = config.title || "Foo";
  config.body = config.body || "Bar";
  config.buttonText = config.buttonText || "Baz";
  config.cancellable = config.cancellable === undefined ? config.cancellable : true;
}

createMenu(menuConfig);
```

### 并发

#### Async/Await 是较 Promises 更好的选择

Promises 是较回调而言更好的一种选择，但 ES7 中的 async 和 await 更胜过 Promises。

在能使用 ES7 特性的情况下可以尽量使用他们替代 Promises。

```js
//正例：
async function getCleanCodeArticle() {
  try {
    var request = await require("request-promise");
    var response = await request.get("https://en.wikipedia.org/wiki/Robert_Cecil_Martin");
    var fileHandle = await require("fs-promise");

    await fileHandle.writeFile("article.html", response);
    console.log("File written");
  } catch (err) {
    console.log(err);
  }
}

//反例：
require("request-promise")
  .get("https://en.wikipedia.org/wiki/Robert_Cecil_Martin")
  .then(function (response) {
    return require("fs-promise").writeFile("article.html", response);
  })
  .then(function () {
    console.log("File written");
  })
  .catch(function (err) {
    console.error(err);
  });
```

### 注释

#### 只对存在一定业务逻辑复杂性的代码进行注释

注释并不是必须的，好的代码是能够让人一目了然，不用过多无谓的注释。

```js
//正例：
function hashIt(data) {
  var hash = 0;
  var length = data.length;

  for (var i = 0; i < length; i++) {
    var char = data.charCodeAt(i);
    hash = (hash << 5) - hash + char;

    // Convert to 32-bit integer
    hash = hash & hash;
  }
}

//反例：
function hashIt(data) {
  // The hash
  var hash = 0;

  // Length of string
  var length = data.length;

  // Loop through every character in data
  for (var i = 0; i < length; i++) {
    // Get character code.
    var char = data.charCodeAt(i);
    // Make the hash
    hash = (hash << 5) - hash + char;
    // Convert to 32-bit integer
    hash = hash & hash;
  }
}
```

#### 函数可使用 jsDoc 进行代码注释

[jsDoc](https://jsdoc.zcopy.site/)

```js
/**
 * 返回一本书.
 * @param {string} title - 书本的标题.
 * @param {string} author - 书本的说明
 */
function Book(title, author) {}
```

### 括号

下列关键字后必须有大括号（即使代码块的内容只有一行）：if, else, for, while, do, switch, try, catch, finally, with。

### jshint

- 用'===', '!=='代替'==', '!='；
- 不要在内置对象的原型上添加方法，如 Array, Date；
- 不要在内层作用域的代码里声明了变量，之后却访问到了外层作用域的同名变量；
- 不要在一些不需要的地方加括号，例：delete(a.b)；
- 不要声明了变量却不使用；
- 不要在应该做比较的地方做赋值；
- debugger 不要出现在提交的代码里；
- 不要在循环内部声明函数；

### 杂项

- 对上下文 this 的引用只能使用'\_this', 'that', 'self'其中一个来命名；
- switch 的 falling through 和 no default 的情况一定要有注释特别说明；
