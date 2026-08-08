- [Vue 基础学习笔记（2）](#vue-基础学习笔记2)
  - [一、指令修饰符](#一指令修饰符)
    - [1. 什么是指令修饰符](#1-什么是指令修饰符)
    - [① 键盘修饰符](#-键盘修饰符)
    - [② v-model 修饰符](#-v-model-修饰符)
    - [③ 事件修饰符](#-事件修饰符)
    - [代码示例：@keyup.enter 监听键盘回车](#代码示例keyupenter-监听键盘回车)
    - [代码示例：v-model 修饰符（.trim .number）](#代码示例v-model-修饰符trim-number)
    - [代码示例：@事件名.stop → 阻止冒泡](#代码示例事件名stop--阻止冒泡)
    - [代码示例：@事件名.prevent → 阻止默认行为](#代码示例事件名prevent--阻止默认行为)
  - [二、v-bind 对样式控制的增强 — 操作 class](#二v-bind-对样式控制的增强--操作-class)
    - [语法](#语法)
    - [① 对象 → 键就是类名，值是布尔值](#-对象--键就是类名值是布尔值)
    - [② 数组 → 数组中所有的类，都会添加到盒子上](#-数组--数组中所有的类都会添加到盒子上)
    - [代码示例](#代码示例)
  - [三、v-bind 对样式控制的增强 — 操作 style](#三v-bind-对样式控制的增强--操作-style)
    - [语法](#语法-1)
    - [代码示例](#代码示例-1)
  - [四、进度条变化的例子](#四进度条变化的例子)
  - [五、v-model 应用于其他表单元素](#五v-model-应用于其他表单元素)
    - [输入框 / 文本域 / 复选框 / 单选框 / 下拉菜单](#输入框--文本域--复选框--单选框--下拉菜单)
    - [代码示例](#代码示例-2)
  - [六、计算属性 computed](#六计算属性-computed)
    - [1. 概念](#1-概念)
    - [2. 语法](#2-语法)
    - [3. computed 计算属性 vs methods 方法](#3-computed-计算属性-vs-methods-方法)
    - [4. 有关 js 中 reduce 的完整语法](#4-有关-js-中-reduce-的完整语法)
    - [代码示例：礼物清单（computed + reduce）](#代码示例礼物清单computed--reduce)
    - [5. 计算属性完整写法](#5-计算属性完整写法)
    - [代码示例：姓名拆分](#代码示例姓名拆分)
  - [七、watch 侦听器（监视器）](#七watch-侦听器监视器)
    - [1. 作用](#1-作用)
    - [2. 语法](#2-语法-1)
    - [① 简单写法](#-简单写法)
    - [代码实例：翻译框](#代码实例翻译框)
    - [② 完整写法 → 添加额外配置项](#-完整写法--添加额外配置项)
  - [八、Vue 的生命周期及四个阶段](#八vue-的生命周期及四个阶段)
    - [1. Vue 生命周期](#1-vue-生命周期)
    - [2. 四个阶段](#2-四个阶段)
    - [3. 何时可发送初始化请求（越早越好）](#3-何时可发送初始化请求越早越好)
    - [4. 生命周期钩子](#4-生命周期钩子)
  - [九、工程化开发 \& 脚手架 Vue CLI](#九工程化开发--脚手架-vue-cli)
    - [工程化开发模式](#工程化开发模式)
    - [Vue CLI 基本介绍](#vue-cli-基本介绍)
    - [使用步骤](#使用步骤)
  - [十、项目目录介绍 \& 运行流程](#十项目目录介绍--运行流程)
    - [index.html 中](#indexhtml-中)
    - [main.js](#mainjs)
  - [十一、组件化开发 \& 根组件](#十一组件化开发--根组件)
    - [1. 组件化](#1-组件化)
    - [2. 根组件](#2-根组件)
    - [3. App.vue 文件（单文件组件）的三个组成部分](#3-appvue-文件单文件组件的三个组成部分)
  - [十二、普通组件的注册 — 局部注册](#十二普通组件的注册--局部注册)
    - [1. 局部注册](#1-局部注册)
    - [2. 使用](#2-使用)
    - [示例：App.vue](#示例appvue)
    - [在 src 下新建 components 文件夹，继续在 components 底下新建 HmHeader \& HmMain \& HmFooter](#在-src-下新建-components-文件夹继续在-components-底下新建-hmheader--hmmain--hmfooter)
      - [HmHeader.vue：](#hmheadervue)
  - [十三、普通组件的注册 — 全局注册](#十三普通组件的注册--全局注册)
    - [1. 全局注册](#1-全局注册)
    - [2. 例：main.js](#2-例mainjs)
    - [3. 在 components 里面新建 HmButton.vue](#3-在-components-里面新建-hmbuttonvue)
  - [十四、组件三大组成部分 — 注意点说明](#十四组件三大组成部分--注意点说明)
    - [scoped 样式冲突](#scoped-样式冲突)
    - [例子](#例子)
      - [App.vue：](#appvue)
      - [BaseOne.vue](#baseonevue)
      - [BaseTwo.vue](#basetwovue)
  - [十五、scoped 原理](#十五scoped-原理)

# Vue 基础学习笔记（2）

---

## 一、指令修饰符

### 1. 什么是指令修饰符
通过 "." 指明一些指令的后缀，不同后缀封装了不同的处理操作 → 简化代码

---

### ① 键盘修饰符
- `@keyup.enter` → 键盘回车监听

---

### ② v-model 修饰符
- `v-model.trim` → 去除首尾空格
- `v-model.number` → 转数字

---

### ③ 事件修饰符
- `@事件名.stop` → 阻止冒泡
- `@事件名.prevent` → 阻止默认行为

---

### 代码示例：@keyup.enter 监听键盘回车

```html
<body>
  <div id="app">
    <h3>@keyup.enter → 监听键盘回车事件</h3>
    <input @keyup.enter="fn" v-model="username" type="text">
  </div>

  <script src="..."></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        username: ''
      },
      methods: {
        fn() {
          console.log('键盘回车的时候触发', this.name)
        }
      }
    })
  </script>
</body>
```

**底层逻辑**：`@keyup.enter` 相当于封装了一层代码：

若无 `.enter`，则 `@keyup`：
```js
methods: {
  fn(e) {
    if (e.key === "Enter") {
      console.log('键盘回车的时候触发', this.username)
    }
  }
}
```

> **补充**：除了 `.enter`，常用的键盘修饰符还有 `.tab`、`.delete`（捕获"删除"和"退格"键）、`.esc`、`.space`、`.up`、`.down`、`.left`、`.right` 等。

---

### 代码示例：v-model 修饰符（.trim .number）

```html
<body>
  <div id="app">
    <h3>v-model修饰符 .trim .number</h3>
    姓名：<input v-model.trim="username" type="text"><br>
    年纪：<input v-model.number="age" type="text"><br>
  </div>

  <script src="..."></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        username: '',
        age: ''
      },
      methods: {
        fatherFn() {
          alert('父亲被点击')
        },
        sonFn() {
          alert('儿子被点击')
        }
      }
    })
  </script>
</body>
```

---

### 代码示例：@事件名.stop → 阻止冒泡

```html
<body>
  <div id="app">
    <h3>@事件名.stop → 阻止冒泡</h3>
    <div @click="fatherFn" class="father">
      <div @click.stop="sonFn" class="son">son</div>
    </div>
  </div>

  <script src="..."></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        username: '',
        age: ''
      },
      methods: {
        fatherFn() {
          alert('父亲被点击')
        },
        sonFn() {
          alert('儿子被点击')
        }
      }
    })
  </script>
</body>
```

---

### 代码示例：@事件名.prevent → 阻止默认行为

```html
<body>
  <div id="app">
    <h3>@事件名.prevent → 阻止默认行为</h3>
    <a @click.prevent href="http://www.baidu.com">阻止默认行为</a>
  </div>

  <script src="..."></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        // ...
      },
      methods: {
        // ...
      }
    })
  </script>
</body>
```

> **补充**：事件修饰符可以链式使用，比如 `@click.stop.prevent` 既阻止冒泡又阻止默认行为。

---

## 二、v-bind 对样式控制的增强 — 操作 class

### 语法
`:class = "对象 / 数组"`

---

### ① 对象 → 键就是类名，值是布尔值
- 值为 `true`，有这个类
- 值为 `false`，否则没这个类

适用场景：一个类，来回切换

```html
<div class="box" :class="{ 类名1: 布尔值, 类名2: 布尔值2 }"></div>
```

---

### ② 数组 → 数组中所有的类，都会添加到盒子上
本质就是一个 class 列表

适用场景：批量添加或删除类

```html
<div class="box" :class="[类名1, 类名2, 类名3]"></div>
```

---

### 代码示例

```html
<head>
  <style>
    .box {
      width: 200px;
      height: 200px;
      border: 3px solid #000;
      font-size: 30px;
      margin-top: 10px;
    }
    .pink {
      background-color: pink;
    }
    .big {
      width: 300px;
      height: 300px;
    }
  </style>
</head>
<body>
  <div id="app">
    <div class="box" :class="{ pink: true, big: true }">你好</div>
    <div class="box" :class="['pink', 'big']">你好</div>
  </div>

  <script src="..."></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        // ...
      }
    })
  </script>
</body>
```

> **补充**：对象写法和数组写法可以混用，比如 `:class="['box', { pink: isPink }]"`。

---

## 三、v-bind 对样式控制的增强 — 操作 style

### 语法
`:style = "样式对象"`

```html
<div class="box" :style="{ css属性名: css属性值, ... }"></div>
```

适用场景：某个具体属性的动态设置

---

### 代码示例

```html
<style>
  .box {
    width: 200px;
    height: 200px;
    background-color: pink;
  }
</style>

<body>
  <div id="app">
    <div class="box" :style="{ width: '400px', height: '400px', backgroundColor: 'green' }"></div>
  </div>
</body>
```

>  **注意**：
> 1. CSS 属性名如果有短横线（如 `background-color`），在对象写法中要改成驼峰命名 `backgroundColor`，或者用引号包起来 `'background-color'`。
> 2. 数值类属性如果不加单位，默认是 `px`，也可以手动写单位，比如 `width: '50%'`。

---

## 四、进度条变化的例子

```css
/* css */
.inner {
  width: 50%;
  height: 20px;
  border-radius: 10px;
  text-align: right;
  position: relative;
  background-color: blue;
  background-size: 24px 24px;
  box-sizing: border-box;
  transition: all 1s;
}
.progress {
  height: 25px;
  width: 400px;
  border-radius: 15px;
  background-color: black;
  border: 2px solid black;
  box-sizing: border-box;
  margin-bottom: 30px;
}
```

```html
<body>
  <div id="app">
    <!-- 外层盒子底色（黑色） -->
    <div class="progress">
      <!-- 内层盒子 - 进度（蓝色） -->
      <div class="inner" :style="{ width: percent + '%' }">
        <span>{{ percent }}%</span>
      </div>
    </div>
    <button @click="percent = 25">设置25%</button>
    <button @click="percent = 50">设置50%</button>
    <button @click="percent = 75">设置75%</button>
    <button @click="percent = 100">设置100%</button>
  </div>

  <script src="..."></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        percent: 30
      }
    })
  </script>
</body>
```

---

## 五、v-model 应用于其他表单元素

常见的表单元素都可以用 `v-model` 绑定关联 → 快速获取或设置表单元素的值。

它会根据**控件类型**自动选取正确的方法来更新元素。

---

### 输入框 / 文本域 / 复选框 / 单选框 / 下拉菜单

| 元素 | v-model 绑定的值 |
|------|-----------------|
| `input:text` | value 值 |
| `textarea` | value 值 |
| `input:checkbox` → 复选框 | checked（布尔值） |
| `input:radio` → 单选框 | value 值 |
| `select` → 下拉菜单 | value 值 |

> **补充**：
> - 复选框如果是**单个**使用，v-model 绑定的是布尔值（是否选中）；
> - 复选框如果是**多个一组**使用，v-model 绑定的是数组（存所有选中项的 value）。
> - 你的笔记里只写了"checked"，没有区分单个和多个的情况，这里补充一下。

---

### 代码示例

```html
<div id="app">
  <h3>信息网</h3>
  姓名：<input type="text" v-model="username">
  <br><br>

  自我介绍：<textarea v-model="desc"></textarea>
  <button>立即注册</button>
  <br><br>

  是否单身：<input type="checkbox" v-model="isSingle">
  <br><br>

  <!-- 
    前置理解：
      1. name: 给单选框加上 name 属性，可以分组 → 同一组互相会互斥
      2. value: 给单选框加上 value 属性，用于给后台传值
  -->
  性别：<input type="radio" name="gender" v-model="gender" value="1">男
       <input type="radio" name="gender" v-model="gender" value="2">女
  <br><br>

  <!-- 
    居住城市：v-model="cityId"
    option 需要 value 属性，提交给后台
    select 关联选中的 option 的 value 值
  -->
  <select v-model="cityId">
    <option value="101">北京</option>
    <option value="102">上海</option>
    <option value="103">成都</option>
    <option value="104">南京</option>
  </select>
  <br><br>
</div>

<script src="..."></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      username: '',
      isSingle: true,
      gender: '1',
      cityId: '102',
      desc: ''
    }
  })
</script>
```

---

## 六、计算属性 computed

### 1. 概念
基于现有的数据，计算出来的新属性。依赖的数据变化，自动重新计算。

### 2. 语法
① 声明在 `computed` 配置项中，一个计算属性对应一个函数
② 使用起来和普通属性一样使用（计算属性名）

```
Computed: {
  计算属性名() {
    基于拥有数据，编写求值逻辑
    return 结果
  }
}
```

---

### 3. computed 计算属性 vs methods 方法
- `computed` 封装了一段对于数据的处理，求得一个结果
- `methods` 方法：给实例提供一个方法，调用以处理业务逻辑

**computed 具有缓存特性（提升性能）**：计算属性会对计算出来的结果缓存，再次使用直接读取缓存，依赖项变化了，会自动重新计算 → 并再次缓存。

>  **补充**：
> - 计算属性是**基于它们的响应式依赖进行缓存的**，只有依赖变化才会重新求值。
> - 方法 `methods` 每次触发重新渲染时，调用方法总会再次执行函数。
> - 所以如果一个计算逻辑比较复杂、又会被多次使用，优先用 computed，性能更好。

---

### 4. 有关 js 中 reduce 的完整语法

```
arr.reduce(callback(accumulator, currentValue, currentIndex, array), initialValue)
```

- `callback`：遍历数组时执行的函数
  - `accumulator`：累计器（上一次返回的值）
  - `currentValue`：当前正在处理的元素
  - `currentIndex`：当前索引（可选）
  - `array`：原数组（可选）
- `initialValue`：初始值（可选）

>  **补充**：如果提供了 `initialValue`，accumulator 的初始值就是 initialValue，currentValue 从数组第一个元素开始；如果没提供 initialValue，accumulator 初始值是数组第一个元素，currentValue 从第二个元素开始。**实际开发中建议始终提供初始值**，避免数组为空时报错。

---

### 代码示例：礼物清单（computed + reduce）

```html
<body>
  <div id="app">
    <h3>礼物清单</h3>
    <table>
      <thead>
        <tr>
          <th>名字</th>
          <th>数量</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in list" :key="item.id">
          <td>{{ item.name }}</td>
          <td>{{ item.num }}</td>
        </tr>
      </tbody>
    </table>
    <p>礼物总数：{{ totalCount }} 个</p>
  </div>

  <script src="..."></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        list: [
          { id: 1, name: '篮球', num: 1 },
          { id: 2, name: '玩具', num: 2 },
          { id: 3, name: '铅笔', num: 5 }
        ]
      },
      computed: {
        totalCount() {
          let total = this.list.reduce((sum, item) => sum + item.num, 0)
          return total
        }
      }
    })
  </script>
</body>
```

---

### 5. 计算属性完整写法

计算属性默认的简写，只能读取访问，不能修改。

完整写法：
```js
computed: {
  计算属性名: {
    get() {
      // 一段代码逻辑（计算逻辑）
      return 结果
    },
    set(修改的值) {
      // 一段代码逻辑（修改逻辑）
    }
  }
}
```

>  **补充**：计算属性的完整写法（getter/setter）用得不多，一般场景用简写就够了。只有当你需要**主动给计算属性赋值**的时候才会用到完整写法的 set。

---

### 代码示例：姓名拆分

```html
<div id="app">
  姓：<input type="text" v-model="firstName"> +
  名：<input type="text" v-model="lastName"> =
  <span>{{ fullName }}</span><br><br>

  <button @click="changeName">改名</button>
</div>

<script src="..."></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      firstName: '刘',
      lastName: '备'
    },
    methods: {
      changeName() {
        this.fullName = '吕布'
      }
    },
    computed: {
      fullName: {
        get() {
          return this.firstName + this.lastName
        },
        set(value) {
          this.firstName = value.slice(0, 1)
          this.lastName = value.slice(1)
        }
      }
    }
  })
</script>
```

> 💡**补充**：JS 里 `slice` 就是截取数组/字符串，不修改原数据。
> - `arr.slice(startIndex, endIndex)` — 数组 slice 语法
> - `str.slice(startIndex, endIndex)` — 字符串 slice 语法
> - `startIndex`：开始截取的位置（包含）
> - `endIndex`：结束位置（不包含），可选，不传就截到最后

---

## 七、watch 侦听器（监视器）

### 1. 作用
监视数据变化，执行一些业务逻辑或异步操作。

### 2. 语法
① 简单写法 → 简单类型数据，直接监视
② 完整写法 → 添加额外配置项

---

### ① 简单写法

格式：
```js
data: {
  words: '苹果',
  obj: {
    words: '苹果'
  }
},
watch: {
  // 该方法会在数据变化时，触发执行
  数据属性名(newValue, oldValue) {
    一些业务逻辑 或 异步操作
  },
  '对象.属性名'(newValue, oldValue) {
    一些业务逻辑 或 异步操作
  }
}
```

>  **补充**：
> - `newValue` 是新值，`oldValue` 是老值
> - 如果只需要新值，可以只写一个参数 `newValue`
> - 监视对象的单个属性时，要用**字符串形式**的键名，比如 `'obj.words'`

---

### 代码实例：翻译框

```html
<!-- 翻译框 -->
<div class="box">
  <div class="input-wrap">
    <textarea v-model="words"></textarea>
    <span>文档翻译</span>
  </div>
  <div class="output-wrap">
    <div class="transbox">mela</div>
  </div>
</div>
```

```js
<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
<!-- 引入Vue框架核心库 -->
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
<!-- 引入axios网络请求库 -->
<script>
  const app = new Vue({
    el: '#app',
    data: {
      obj: {
        words: ''
      },
      words:''
    },
    watch: {
      // 该方法会在数据变化时调用执行
      words(newValue) {
        console.log('变化了', newValue) // newValue新值, oldValue老值（一般不用）
      },
      'obj.words'(newValue) {
        console.log('变化了', newValue)
      }
    }
  })
</script>
```

> `watch` 里同时写了 `words` 和 `'obj.words'` 两个侦听器。实际使用时根据你的数据结构选一种就行，不用两个都写。

---

### ② 完整写法 → 添加额外配置项

1. `deep: true` → 对复杂类型深度监视
2. `immediate: true` → 初始化立刻执行一次 handler 方法

>  **补充**：
> - `deep` 深度监视：当监视的是一个对象/数组时，默认只监视整个引用的变化（整个对象替换才触发）。加了 `deep: true` 之后，对象内部任何属性变化都会触发。
> - `immediate` 立即执行：默认 watch 只有在数据变化时才触发，加了 `immediate: true` 之后，页面一加载就会先执行一次。
> - 完整写法中，处理函数的名字固定叫 `handler`。

---

## 八、Vue 的生命周期及四个阶段

### 1. Vue 生命周期
一个 Vue 实例从创建到销毁的整个过程。

### 2. 四个阶段
① **创建阶段**：把普通数据转为响应式数据
② **挂载阶段**：渲染模板
③ **更新阶段**：数据修改，更新视图（可执行多次）
④ **销毁阶段**：销毁实例

### 3. 何时可发送初始化请求（越早越好）
→ 创建阶段最后

何时可操作 dom（至少要 dom 渲染出来）
→ 挂载阶段最后

### 4. 生命周期钩子
- `beforeCreate`
- `created`
- `beforeMount`
- `mounted`
- `beforeUpdate`
- `updated`
- `beforeDestroy`
- `destroyed`

```
beforeCreate → created → beforeMount → mounted → beforeUpdate → updated → beforeDestroy → destroyed
    ① 创建阶段        ② 挂载阶段          ③ 更新阶段（可多次）         ④ 销毁阶段
```

> **补充**：
> - **created**：最早可以发送网络请求的钩子（数据已经是响应式了，但 DOM 还没渲染）
> - **mounted**：最早可以操作 DOM 的钩子（模板已经渲染成真实 DOM 了）
> - 实际开发中，**发送初始化数据请求一般放在 created 里**，这样能更早拿到数据，用户等待时间更短。
> - 你的笔记里写"创建阶段最后"发请求，就是指 `created` 这个钩子，没错。

>  **小提醒**：Vue 3 中生命周期钩子名字有变化，比如 `mounted` 变成了 `onMounted`（组合式 API 写法），这个是 Vue 2，所以上面就是对的。

---

## 九、工程化开发 & 脚手架 Vue CLI

### 工程化开发模式
基于构建工具（例如 webpack）的环境中开发 Vue。

```
源代码 → 自动化编译打包组合 → 运行的代码
  es6语法/typescript           js(es3/es5)
  less/sass                    css
  问题：① webpack 配置不简单
        ② 需同的基础配置
        ③ 缺乏统一标准
需要一个工具，生成标准化的配置
```

---

### Vue CLI 基本介绍
Vue CLI 是 Vue 官方提供的全局命令工具。
→ 可帮助我们快速创建一个开发 Vue 项目的标准化基础架子。
→ 集成了 webpack 配置

**基础架子**：① 开箱即用，0 配置  ② 内置 babel 等工具  ③ 标准化

---

### 使用步骤
① 全局安装（一次）：
```
yarn global add @vue/cli
或
npm i @vue/cli -g
```

② 查看 vue 版本：
```
vue --version
```

③ 创建项目架子：
```
vue create project-name（不用中文）
```

④ 启动项目：
```
yarn serve
或
npm run serve
（找 package.json）
```

>  **补充**：
> - 安装 CLI 是全局安装，只需要装一次，以后创建项目都能用。
> - `vue create 项目名` 创建项目时，会让你选 Vue 2 还是 Vue 3，注意选你学的版本。
> - 启动命令 `yarn serve` / `npm run serve` 必须在**项目根目录**下执行。

---

## 十、项目目录介绍 & 运行流程

### index.html 中

```html
<body>
  <!-- 兼容：给不支持 js 的浏览器一个提示 -->
  <noscript>
    <strong>We're sorry but <%= htmlWebpackPlugin.options.title %> doesn't work properly without JavaScript enabled. Please enable it to continue.</strong>
  </noscript>
  <!-- Vue 所管理的容器：将来创建结构，动态渲染内容 -->
  <div id="app"></div>
  <!-- 在工程化开发模式中：此处不再直接编写模板语法，而是通过 App.vue 提供结构渲染 -->
</body>
```

---

### main.js

```js
// 文件核心作用：导入 App.vue，基于 App.vue 创建结构渲染 index.html

// 1. 导入 Vue 核心包
import Vue from 'vue'
// 2. 导入 App Vue 根组件
import App from './App.vue'

// 提示：当前处于什么环境（生产环境 / 开发环境）
Vue.config.productionTip = false

// Vue 实例化，提供 render 方法 → 基于 App.vue 创建结构渲染
new Vue({
  render: h => h(App),
}).$mount('#app')
```

> 与这个写法效果一样：
```js
new Vue({
  el: '#app', // 作用和 $mount('选择器') 作用一致，用于指定 Vue 所管理容器
  render: h => h(App),
  // render: h => h(App) 是简写
  // 完整写法：render: ccreateElement => {
  //   // 基于 App 创建元素结构
  //   return createElement(App)
  // }
}).$mount('#app')
```

>  **补充**：
> - `render: h => h(App)` 是 Vue 渲染函数的简写形式，`h` 就是 `createElement` 的别名。
> - `$mount('#app')` 和 `el: '#app'` 作用完全一样，都是把 Vue 实例挂载到页面上的某个容器。
> - 工程化项目里用 `$mount` 是为了更灵活（比如可以先做一些异步操作再挂载）。

---

## 十一、组件化开发 & 根组件

### 1. 组件化
一个页面可以拆分成一个个组件，每个组件有着自己独立的结构、样式、行为。

**好处**：便于维护，利于复用 → 提升开发效率

### 2. 根组件
整个应用最上层的组件，包裹所有普通小组件

### 3. App.vue 文件（单文件组件）的三个组成部分
① 语法高亮插件
② 三部分组成
- `template`：结构（有且只能一个根元素）(Vue2)
- `script`：js 逻辑
- `style`：样式（可支持 less，需要装包）

③ 让组件支持 less
- a. style 标签，`lang="less"` 开启 less 功能
- b. 装包：`yarn add less less-loader`

```vue
<style lang="less">
#App {
  width: 400px;
  height: 400px;
  background-color: pink;

  .box {
    width: 100px;
    height: 100px;
    background-color: skyblue;
  }
}
</style>
```

>  **补充**：
> - Vue 2 中 `template` 里**必须只有一个根元素**，如果有多个元素要包在一个父 div 里。
> - Vue 3 中支持多根元素（Fragment），不用包了。


---

## 十二、普通组件的注册 — 局部注册

### 1. 局部注册
只能在注册的组件内使用

① 创建 .vue 文件（三个组成部分）
② 在使用的组件内导入并注册

例子：
```js
// 1. 导入需要注册的组件
import 组件对象 from '.vue文件路径'
import HmHeader from './components/HmHeader'

export default {
  // 局部注册
  components: {
    // 组件名: 组件对象
    HmHeader: HmHeader
  }
}
```

### 2. 使用
把组件名当成 html 标签使用 `<组件名></组件名>`

**注意**：组件名规范 → 大驼峰命名法，如：`HmHeader`

---

### 示例：App.vue

```vue
<template>
  <div class="App">
    <!-- 头部组件 -->
    <HmHeader></HmHeader>
    <!-- 主体组件 -->
    <HmMain></HmMain>
    <!-- 底部组件 -->
    <HmFooter></HmFooter>
  </div>
</template>

<script>
import HmHeader from './components/HmHeader.vue'
import HmMain from './components/HmMain.vue'
import HmFooter from './components/HmFooter.vue'

export default {
  components: {
    // 组件名: 组件对象
    HmHeader: HmHeader,
    HmMain, // 等同于 HmMain: HmMain
    HmFooter
  }
}
</script>

<style>
#App {
  width: 600px;
  height: 700px;
  background-color: #87ceeb;
  margin: 0 auto;
  padding: 20px;
}
</style>
```

>  **补充**：
> - `components` 里的组件注册可以用**对象简写**，当组件名和导入的变量名一样时，可以只写一个，比如 `HmMain` 就是 `HmMain: HmMain` 的简写。
> - 组件名推荐用**大驼峰（PascalCase）**，在模板里使用时既可以写大驼峰 `<HmHeader />`，也可以写短横线 `<hm-header />`，两种都可以。

---

### 在 src 下新建 components 文件夹，继续在 components 底下新建 HmHeader & HmMain & HmFooter

#### HmHeader.vue：
```vue
<template>
  <div class="hm-header">
    hm-header
  </div>
</template>

<script>
export default {

}
</script>

<style>
.hm-header {
  height: 100px;
  line-height: 100px;
  text-align: center;
  font-size: 30px;
  background-color: #8064a2;
  color: white;
}
</style>
```

> HmMain.vue 与 HmFooter.vue 写法与 HmHeader.vue 类似

> **小技巧**：如果 HmFooter + tab 出不来 → 则配置 vscode，在设置（左下角）中搜：`trigger on tab` → 打开

---

## 十三、普通组件的注册 — 全局注册

### 1. 全局注册
所有组件内都能使用

① 创建 .vue 文件（三个组成部分）
② main.js 中进行全局注册

格式：
```js
// 1. 导入需要全局注册的组件
import HmButton from './components/HmButton'
// 调用 Vue.component 进行全局注册
Vue.component('组件名', 组件对象)
Vue.component('HmButton', HmButton)
```

### 2. 例：main.js

```js
import Vue from 'vue'
import App from './App.vue'

// 编写导入的代码，往代码的顶部编写（规范）
import HmButton from './components/HmButton'

Vue.config.productionTip = false

// 进行全局注册
Vue.component('HmButton', HmButton)

new Vue({
  // ...
})
```

### 3. 在 components 里面新建 HmButton.vue

```vue
<template>
  <button class="hm-button">通用按钮</button>
</template>

<script>
export default {

}
</script>

<style>
.hm-button {
  height: 50px;
  line-height: 50px;
  padding: 0 20px;
  background-color: #3bae56;
  border-radius: 5px;
  border: none;
}
</style>
```

此时即可在 HmFooter.vue 中：
```
// 在 <template></template> 中的 <div></div> 内写上
<HmButton></HmButton>
// 在 HmMain.vue 和 HmHeader.vue 中也可用
```

> **补充**：
> - **局部注册**：用得更多，按需引入，打包体积更小，更推荐。
> - **全局注册**：适合那些**很多页面都要用到的通用组件**（比如按钮、弹窗、图标等），但全局注册的组件就算你不用也会被打包进去，所以不要什么都全局注册。
> - 实际项目中：通用组件全局注册，业务组件局部注册。

---

## 十四、组件三大组成部分 — 注意点说明

① 结构 `<template>`：只能有一个根元素

② 样式 `<style>`：全局样式（默认）→ 影响所有组件
   局部样式：scoped 样式，只作用于当前组件

③ 逻辑 `<script>`：el 根实例独有，data 是一个函数，其他配置项一致

---

### scoped 样式冲突

默认情况：写在组件中的样式会全局生效 → 因此很容易造成多个组件之间的样式冲突问题。

① 全局样式：默认组件中的样式会作用到全局
② 局部样式：可以给组件加上 scoped 属性，可以让样式只作用于当前组件

---

### 例子

#### App.vue：
```vue
<template>
  <div id="app">
    <BaseOne></BaseOne>
    <BaseTwo></BaseTwo>
  </div>
</template>

<script>
import BaseOne from './components/BaseOne.vue'
import BaseTwo from './components/BaseTwo.vue'

export default {
  name: 'App',
  components: {
    BaseOne,
    BaseTwo
  }
}
</script>
```

#### BaseOne.vue
```vue
<template>
  <div>BaseOne</div>
</template>

<script>
export default {

}
</script>

<style scoped>
/* 1. 默认的 style 样式，会作用于全局 → 全局样式
   2. 加上 scoped 属性的 style 样式，只会作用于当前组件 → 局部样式
   组件应该有着自己独立的样式 → 推荐加上 scoped */
div {
  border: 3px solid blue;
  margin: 30px;
}
</style>
```

#### BaseTwo.vue
```vue
<template>
  <div>BaseTwo</div>
</template>

<script>
export default {

}
</script>

<style scoped>
div {
  border: 3px solid red;
  margin: 30px;
}
</style>
```

>  **补充**：
> - 开发中**每个组件的 style 都建议加上 scoped**，避免样式互相污染。
> - 这是 Vue 单文件组件的最佳实践之一。

---

## 十五、scoped 原理

1. 给当前组件模板的所有元素，都会添加上一个自定义属性 `data-v-hash值`（不同的哈希值可区分开不同的组件）
2. CSS 选择器后面，被自动处理，添加上了属性选择器

如：`div[data-v-5f6a9d56]`

// 在 BaseOne.vue 中若把 `<div></div>` 改成
```vue
<div>BaseOne
  <span>111</span>
  <a href="">链接</a>
</div>
```
// 里面的 span 和 链接也会被同步原样式（蓝边框）

> **补充**：
> - scoped 的原理就是通过 **data-v-xxx 自定义属性 + 属性选择器** 实现样式隔离。
> - 每个组件的 hash 值不一样，所以样式不会互相影响。
> - 子组件的**根元素**会同时继承父组件和子组件的 data-v 属性（因为父组件渲染时也把它当自己的一个元素），这就是为什么有时候父组件的样式能影响到子组件根元素。
> - 如果想在 scoped 样式里**穿透**影响子组件的内部样式，可以用 `::v-deep` 或 `/deep/`（Vue 2 中），但不能滥用。
