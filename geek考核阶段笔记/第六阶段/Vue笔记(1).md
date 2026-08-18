- [Vue 基础学习笔记（1）](#vue-基础学习笔记1)
  - [1. Vue 的定义](#1-vue-的定义)
    - [Vue 的两种使用方式](#vue-的两种使用方式)
  - [2. 创建 Vue 实例，初始化渲染](#2-创建-vue-实例初始化渲染)
    - [步骤](#步骤)
    - [基础代码](#基础代码)
    - [响应式](#响应式)
  - [3. 插值表达式](#3-插值表达式)
    - [代码示例](#代码示例)
  - [4. Vue 指令](#4-vue-指令)
    - [① v-html](#-v-html)
    - [② v-show 与 v-if](#-v-show-与-v-if)
      - [v-show](#v-show)
      - [v-if](#v-if)
      - [代码示例](#代码示例-1)
    - [③ v-else 和 v-else-if](#-v-else-和-v-else-if)
    - [④ v-on](#-v-on)
      - [a. 内联语句](#a-内联语句)
      - [b. methods 中的函数名](#b-methods-中的函数名)
      - [v-on 调用传参](#v-on-调用传参)
    - [⑤ v-bind](#-v-bind)
      - [代码示例](#代码示例-2)
    - [⑥ v-for](#-v-for)
      - [遍历数组语法](#遍历数组语法)
      - [v-for 中的 key](#v-for-中的-key)
    - [⑦ v-model](#-v-model)
  - [5. 指令修饰符](#5-指令修饰符)
    - [① 键盘事件修饰符](#-键盘事件修饰符)
    - [② v-model 修饰符](#-v-model-修饰符)
    - [③ 事件修饰符](#-事件修饰符)

# Vue 基础学习笔记（1）

---

## 1. Vue 的定义
Vue 是一个用于**构建用户界面**的**渐进式框架**。

- 渐进式：循序渐进，一套完整的项目解决方案（提高开发效率）
- 生态核心：
  - 声明式渲染
  - 组件系统
  - 客户端路由（Vue Router）
  - 大规模状态管理（Vuex）
  - 构建工具（Webpack / Vite）

### Vue 的两种使用方式
1. **Vue 核心包开发**
   - 场景：局部模块改造
2. **Vue 核心包 & Vue 插件，工程化开发**
   - 场景：整体开发

>  **补充**：Vue 2 和 Vue 3 是目前两个主流版本。笔记里用的 CDN 是 `vue@2.7.10`，属于 **Vue 2** 的语法。现在主流新项目已经用 **Vue 3** 了，核心指令逻辑基本一样，但实例创建方式从 `new Vue()` 变成了 `createApp()`

---

## 2. 创建 Vue 实例，初始化渲染

### 步骤
1. 准备容器
2. 引包（官网）— 开发版本 / 生产版本
3. 创建 Vue 实例 `new Vue()`
4. 指定配置项 → 渲染数据
   - `el` 指定挂载点
   - `data` 提供数据

### 基础代码
```html
<div id="app">
  {{ msg }}
</div>

<script src="https://cdn.jsdelivr.net/npm/vue@2.7.10/dist/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      msg: 'Hello',
      nickname: 'tony',
      age: 18,
      friend: {
        name: 'jepson',
        desc: '热爱学习 Vue'
      }
    }
  })
</script>
```


### 响应式
- 数据的响应式处理 → 响应式：数据变化，视图自动更新
- `data` 中的数据，最终会被添加到实例上
  - 访问数据：`实例.属性名`
  - 修改数据：`实例.属性名 = "值"`

```html
<div id="app">
  {{ msg }}  // 你好
</div>

<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      msg: '你好'
    }
  })
</script>
```

`app.msg = '你好，我是...'` → 页面由「你好」→「你好，我是...」

Vue 核心特性：响应式
数据 → 修改数据，监听到数据修改 → 自动更新视图，视图界面 DOM 操作

---

## 3. 插值表达式

1. **作用**：利用表达式进行插值，渲染到页面中
   - 表达式：是可以被求值的代码，JS 引擎会将其计算出一个结果

2. **语法**：`{{ 表达式 }}`

3. **注意**：
   - a. 使用的数据必须存在（data）
     - `<p>{{ hobby }}</p>` （×）
   - b. 支持的是表达式，而非语句，比如：`if` `for` ...
     - `<p>{{ if }}</p>` （×）

     > 更典型的反例： `{{ for(let i=0;i<5;i++){...} }}` 这种完整语句。

   - c. 不能在标签属性中使用 `{{ }}` 插值
     - `<p title="{{ username }}">标签</p>` （×）

### 代码示例
```html
<div id="app">
  <p>{{ nickname }}</p>
  <p>{{ nickname.toUpperCase() }}</p>
  <p>{{ age > 18 ? '成年' : '未成年' }}</p>
</div>

<script src="..."></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      nickname: 'tony',
      age: 18
    }
  })
</script>
```

---

## 4. Vue 指令

Vue 会根据不同的指令，针对标签实现不同的功能。
指令：带有 `v-` 前缀的特殊标签属性。

>  **指令速查表**
> | 指令 | 作用 | 简写 |
> |------|------|------|
> | `v-html` | 设置 innerHTML | - |
> | `v-show` | 显示/隐藏（CSS 切换） | - |
> | `v-if` | 显示/隐藏（DOM 创建/销毁） | - |
> | `v-else / v-else-if` | 辅助 v-if 判断 | - |
> | `v-on` | 绑定事件 | `@` |
> | `v-bind` | 绑定属性 | `:` |
> | `v-for` | 列表渲染 | - |
> | `v-model` | 双向数据绑定 | - |

---

### ① v-html

- 作用：设置元素的 `innerHTML`
- 语法：`v-html = "表达式"`
- 动态解析标签（若用插值表达式的话则会解析失败）

```html
<div id="app">
  <div v-html="msg"></div>
</div>

<script src="..."></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      msg: '<a href="http://www.itheima.com">黑马程序员</a>'
    }
  })
</script>
```

> 动态设置元素的 innerHTML 变量

>  **重要补充**：`v-html` 直接解析 HTML 存在 **XSS 注入风险**，只能在**可信内容**上使用，永远不要用在用户输入的内容上

---

### ② v-show 与 v-if

#### v-show
- 作用：控制元素显示隐藏
- 语法：`v-show="表达式"` → 表达式值 `true` 显示，`false` 隐藏
- 场景：频繁切换显示隐藏的场景

#### v-if
- 作用：控制元素显示隐藏（条件渲染）
- 语法：`v-if="表达式"` → 表达式值 `true` 显示，`false` 隐藏
- 底层原理：根据判断条件，控制元素的创建和移除
- 场景：要么显示，要么隐藏，不频繁切换的场景

#### 代码示例
```html
<head>
  <style>
    .box {
      border: 2px solid black;
      padding: 40px 20px;
      width: 200px;
      display: block;
      margin-bottom: 24px;
      text-align: center;
    }
  </style>
</head>
<body>
  <div id="app">
    <div class="box" v-show="flag">v-show</div>
    <div class="box" v-if="flag">v-if</div>
  </div>

  <script src="..."></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        flag: true
      }
    })
  </script>
</body>
```

> `flag` 为 `true` 时两个盒子均显示，`flag` 为 `false` 时两个盒子均隐藏

- **v-show 底层原理**：切换 CSS 的 `display: none` 来控制显示隐藏
- **v-if 底层原理**：根据判断条件，控制元素的创建和移除

---

### ③ v-else 和 v-else-if

- 作用：辅助 `v-if` 进行判断渲染
- 语法：`v-else` 、 `v-else-if="表达式"`
- 注意：需要紧挨着 `v-if` 使用

```html
<body>
  <div id="app">
    <p v-if="gender === 1">性别：男</p>
    <p v-else>性别：女</p>
    <hr>
    <p v-if="score >= 90">成绩评定A</p>
    <p v-else-if="score >= 70">成绩评定B</p>
    <p v-else-if="score >= 60">成绩评定C</p>
    <p v-else>成绩评定D</p>
  </div>

  <script src="..."></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        gender: 2,
        score: 95
      }
    })
  </script>
</body>
```

输出：
- 性别：女
- 成绩评定A

---

### ④ v-on

- 作用：注册事件 + 添加监听 + 提供处理逻辑
- 语法：
  - a. `v-on:事件名 = "内联语句"`
  - b. `v-on:事件名 = "methods 中的函数名"`

#### a. 内联语句
```html
<body>
  <div id="app">
    <button v-on:click="count--">-</button>
    <span>{{ count }}</span>
    <button v-on:click="count++">+</button>
  </div>

  <script src="..."></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        count: 100
      }
    })
  </script>
</body>
```

> `v-on:` 整体可替换为 `@`

> **补充**：如果内联语句里同时需要**传参**又需要**事件对象**，用 `$event` 占位：
> `@click="fn(参数, $event)"`

#### b. methods 中的函数名
```html
<div id="app">
  <button @click="fn">切换显示隐藏</button>
  <h1 v-show="isShow">黑马程序员</h1>
</div>

<script src="..."></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      isShow: true
    },
    methods: {
      fn() {
        this.isShow = !this.isShow
        // 让提供的所有 methods 中的函数，this 都指向当前 Vue 实例
      }
    }
  })
</script>
```

> `methods` 配置项内可提供很多 Vue 实例当中要使用的方法

#### v-on 调用传参
格式：`<button @click="fn(参数1, 参数2)">按钮</button>`

```html
<body>
  <div id="app">
    <div class="box">
      <h3>自动售货机</h3>
      <button @click="buy(5)">可乐5元</button>
      <button @click="buy(10)">咖啡10元</button>
      <button @click="buy(8)">牛奶8元</button>
    </div>
    <p>银行卡余额：{{ money }}元</p>
  </div>

  <script src="..."></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        money: 100
      },
      methods: {
        buy(price) {
          this.money -= price
        }
      }
    })
  </script>
</body>
```

---

### ⑤ v-bind

- 作用：动态的设置 html 的标签属性（`src`、`url`、`title` ...）
- 语法：`v-bind:属性名="表达式"`

#### 代码示例
```html
<body>
  <div id="app">
    <img v-bind:src="imgUrl" v-bind:title="msg" alt="">
  </div>

  <script src="https://..."></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        imgUrl: './imgs/10-02.png',
        msg: 'hello'
      }
    })
  </script>
</body>
```

> `v-bind:src` 可替换为 `:src`

>  **补充**：`v-bind` 绑定 class 的两种常用写法：
> - **对象写法**：`:class="{ 类名: 布尔值 }"` → 为 `true` 就加这个类
> - **数组写法**：`:class="[类名1, 类名2]"` → 批量加类
> - 两种可以混用：`:class="['box', { pink: isPink }]"`

---

### ⑥ v-for

- 作用：基于数据循环，多次渲染整个元素 → 数组、对象、数字
- `<p v-for="...">我是一个内容</p>`

#### 遍历数组语法
`v-for="(item, index) in 数组"`

- `item` 每一项，`index` 下标

```html
<body>
  <div id="app">
    <h3>水果店</h3>
    <ul>
      <li v-for="(item, index) in list">
        {{ item }} -- {{ index }}
      </li>
    </ul>
  </div>

  <script src="..."></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        list: ['西瓜', '苹果', '鸭梨', '榴莲']
      }
    })
  </script>
</body>
```

> 如果在不需要 `index` 的场景下，可省略 `index` 和括号，只保留 `item`：
> `v-for="item in list"`

#### v-for 中的 key
（v-for 的默认行为会尝试原地修改元素）

- 语法：`key属性 = "唯一标识"`
- 作用：给列表项添加的唯一标识，便于 Vue 进行列表项的正确排序复用

**注意点**：
- a. `key` 的值只能是字符串或数字类型
- b. `key` 的值必须具有唯一性
- c. 推荐使用 `id` 作为 `key`（唯一），不推荐使用 `index` 作为 `key`（会变化，不对应）

>  **补充**：当列表顺序**不会变化**（纯展示、不会增删排序）时，用 index 作 key 也没问题，不会出 bug；只有在**列表会动态增删/排序**时才必须用唯一 id。

---

### ⑦ v-model

- 作用：给表单元素使用，双向数据绑定 → 可快速获取或设置表单元素内容
  - a. 数据变化 → 视图自动更新
  - b. 视图变化 → 数据自动更新

```html
<body>
  <div id="app">
    账号：<input type="text" v-model="username"><br><br>
    密码：<input type="password" v-model="password"><br><br>
    <button @click="login">登录</button>
    <button @click="reset">重置</button>
  </div>

  <script src="..."></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        username: '',
        password: ''
      },
      methods: {
        login() {
          console.log(this.username, this.password)
        },
        reset() {
          this.username = ''
          this.password = ''
        }
      }
    })
  </script>
</body>
```

> **补充**：`v-model` 常用的表单元素远不止 text 和 password：
> - `input[type=text/password]` → 绑定 value
> - `textarea` → 绑定内容
> - `input[type=checkbox]` → 单个绑布尔值，多个一组绑数组
> - `input[type=radio]` → 绑定 value
> - `select` → 绑定选中值

---

## 5. 指令修饰符

通过 `.` 指明一些指令的后缀，不同后缀封装了不同的处理操作 → 简化代码

### ① 键盘事件修饰符
- `@keyup.enter` → 键盘回车监听

### ② v-model 修饰符
- `v-model.trim` → 去除首尾空格
- `v-model.number` → 转数字

### ③ 事件修饰符
- `@事件名.stop` → 阻止冒泡
- `@事件名.prevent` → 阻止默认行为

```html
<body>
  <div id="app">
    <h3>@keyup.enter → 监听键盘回车</h3>
    <input @keyup.enter="fn" type="text">
  </div>

  <script src="..."></script>
  <script>
    // ...
  </script>
</body>
```

>  **补充**：事件修饰符可以链式使用，比如 `@click.stop.prevent` 既阻止冒泡又阻止默认行为。
