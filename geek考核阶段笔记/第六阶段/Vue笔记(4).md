- [Vue2 学习笔记](#vue2-学习笔记)
  - [一、ref 和 $refs](#一ref-和-refs)
    - [作用](#作用)
    - [特点](#特点)
    - [① 获取 dom](#-获取-dom)
    - [② 获取组件](#-获取组件)
  - [二、Vue 异步更新、$nextTick](#二vue-异步更新nexttick)
    - [1、需求：编辑标题，编辑框自动聚焦](#1需求编辑标题编辑框自动聚焦)
    - [2、此写法](#2此写法)
    - [3、$nextTick](#3nexttick)
    - [4、示例](#4示例)
  - [三、自定义指令](#三自定义指令)
    - [1、自定义指令](#1自定义指令)
    - [2、语法](#2语法)
  - [四、自定义指令 — 指令的值](#四自定义指令--指令的值)
    - [1、需求](#1需求)
    - [2、语法](#2语法-1)
    - [3、通过 `binding.value` 可以拿到指令值，指令值修改会触发 `update` 函数](#3通过-bindingvalue-可以拿到指令值指令值修改会触发-update-函数)
    - [4、示例](#4示例-1)
  - [五、自定义指令 — v-loading 指令封装](#五自定义指令--v-loading-指令封装)
    - [1、场景](#1场景)
    - [2、需求](#2需求)
    - [3、分析](#3分析)
    - [4、实现](#4实现)
    - [5、代码示例](#5代码示例)
  - [六、插槽 — 默认插槽](#六插槽--默认插槽)
    - [1、作用](#1作用)
    - [2、需求](#2需求-1)
    - [3、问题](#3问题)
    - [4、语法](#4语法)
    - [5、示例](#5示例)
  - [七、插槽 — 后备内容（默认值）](#七插槽--后备内容默认值)
    - [1、概念](#1概念)
    - [2、语法](#2语法-2)
    - [3、效果](#3效果)
  - [八、插槽 — 具名插槽](#八插槽--具名插槽)
    - [1、需求](#1需求-1)
    - [2、语法](#2语法-3)
    - [3、示例](#3示例)
  - [九、插槽 — 作用域插槽](#九插槽--作用域插槽)
    - [1、定义](#1定义)
    - [2、场景：封装表格组件](#2场景封装表格组件)
    - [3、基本使用步骤](#3基本使用步骤)
    - [4、示例](#4示例-2)
  - [十、单页应用程序 \& 路由介绍](#十单页应用程序--路由介绍)
    - [1、单页 vs 多页对比](#1单页-vs-多页对比)
    - [2、适用场景](#2适用场景)
    - [3、路由的概念](#3路由的概念)
  - [十一、路由的基本使用](#十一路由的基本使用)
    - [1、VueRouter 的使用](#1vuerouter-的使用)
    - [2、2 个核心步骤](#22-个核心步骤)
    - [3、示例](#3示例-1)
    - [4、组件目录的存放](#4组件目录的存放)
  - [十二、路由的封装抽离](#十二路由的封装抽离)
    - [1、目的](#1目的)
    - [2、示例](#2示例)
  - [十三、声明式导航 — 导航链接](#十三声明式导航--导航链接)
    - [1、需求](#1需求-2)
    - [2、vue-router 提供了一个全局组件 router-link（取代 a 标签）](#2vue-router-提供了一个全局组件-router-link取代-a-标签)
    - [3、示例](#3示例-2)
  - [十四、声明式导航 — 两个高亮类名](#十四声明式导航--两个高亮类名)
    - [1、router-link 自动给当前导航添加了 2 个高亮类名](#1router-link-自动给当前导航添加了-2-个高亮类名)
    - [2、两个类名的区别](#2两个类名的区别)

# Vue2 学习笔记

---

## 一、ref 和 $refs

### 作用
利用 `ref` 和 `$refs` 可以用于获取 dom 元素，或组件实例。

### 特点
查找范围 → **当前组件内**（更精确稳定）

### ① 获取 dom

**a、目标标签 — 添加 ref 属性**

```html
<div ref="chartRef">我是渲染图表的容器</div>
```

**b、恰当时机，通过 `this.$refs.xxx` 获取目标标签**

```js
mounted() {
  console.log(this.$refs.chartRef)
}
```

### ② 获取组件

**a、目标组件 — 添加 ref 属性**

```html
<BaseForm ref="baseForm"></BaseForm>
```

**b、恰当时机，通过 `this.$refs.xxx` 获取目标组件，就可以调用组件对象里面的方法**

```js
this.$refs.baseForm.组件方法()
```

> **补充：** `$refs` 只在组件渲染完成后才填充，且它是非响应式的，因此不能在模板中使用，也不能用它做数据绑定。仅适合在生命周期钩子（如 `mounted`）或事件回调中访问。

---

## 二、Vue 异步更新、$nextTick

### 1、需求：编辑标题，编辑框自动聚焦

1. 点击编辑，显示编辑框
2. 让编辑框立刻获取焦点

### 2、此写法

```js
this.isShowEdit = true   // 显示输入框
this.$refs.inp.focus()   // 获取焦点
```

**产生问题：** "显示之后"，立刻获取焦点是不能成功的。

**原因：** Vue 是异步更新 DOM（提升性能）。

### 3、$nextTick

等 DOM 更新后，才会触发执行此方法里的函数体。

**语法：**

```js
this.$nextTick(函数体)
```

>  **补充：** `$nextTick` 也支持 Promise 写法，可配合 `async/await` 使用：
> ```js
> async handleEdit() {
>   this.isShowEdit = true
>   await this.$nextTick()
>   this.$refs.inp.focus()
> }
> ```

### 4、示例

```html
<template>
  <div class="app">
    <!-- 是否在编辑状态 -->
    <div v-if="isShowEdit">
      <input ref="inp" v-model="editValue" type="text">
      <button>确认</button>
    </div>
    <!-- 默认状态 -->
    <div v-else>
      <span>{{title}}</span>
      <button @click="handleEdit">编辑</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: '大标题',
      editValue: '',
      isShowEdit: false
    }
  },
  methods: {
    handleEdit() {
      this.isShowEdit = true
      this.$nextTick(() => {
        this.$refs.inp.focus()
      })
    }
  }
}
</script>

<style scoped>
/* ⚠️ 注意：.logout 类在模板中没有对应元素，属于多余样式，实际使用时可删除 */
.logout {
  margin: 20px;
}
button {
  margin: 10px;
}
</style>
```

---

## 三、自定义指令

### 1、自定义指令

自己定义的指令，可封装一些 dom 操作，扩展额外功能。

**需求：** 当页面加载时，让元素将获得焦点（autofocus 在 Safari 浏览器有兼容性）。

**操作 dom：**

```js
dom元素.focus()

mounted() {
  this.$refs.inp.focus()
}
```

### 2、语法

**a、全局注册**

```js
Vue.directive('指令名', {
  "inserted"(el) {
    // 可以对 el 标签，扩展额外功能
    el.focus()
  }
})
// inserted 指的是当指令所绑定的元素被添加到页面当中时，会自动调用
```

**b、局部注册**

```js
directives: {
  "指令名": {
    inserted(el) {
      el.focus()
    }
  }
}
```

**c、使用方法**

```html
<input v-指令名 type="text">
```

> **补充：** 自定义指令的完整钩子函数共有 5 个：
> - `bind`：指令第一次绑定到元素时调用（只调用一次）
> - `inserted`：被绑定元素插入父节点时调用
> - `update`：所在组件的 VNode 更新时调用（可能发生在子 VNode 更新之前）
> - `componentUpdated`：组件的 VNode 及其子 VNode 全部更新后调用
> - `unbind`：指令与元素解绑时调用（只调用一次）

---

## 四、自定义指令 — 指令的值

### 1、需求

实现一个 `color` 指令 — 传入不同的颜色，给标签设置文字颜色。

### 2、语法

在绑定指令时，可通过"等号"的形式为指令绑定具体的参数值。

```html
<div v-color="color">我是内容</div>
```

### 3、通过 `binding.value` 可以拿到指令值，指令值修改会触发 `update` 函数

```js
directives: {
  color: {
    inserted(el, binding) {
      el.style.color = binding.value
    },
    update(el, binding) {
      el.style.color = binding.value
    }
  }
}
```

### 4、示例

```html
<template>
  <div>
    <h1 v-color="color1">指令的值测试</h1>
    <h1 v-color="color2">指令的值测试</h1>
  </div>
</template>

<script>
export default {
  data() {
    return {
      color1: 'red',
      color2: 'orange'
    }
  },
  directives: {
    color: {
      inserted(el, binding) {
        el.style.color = binding.value
      },
      // update 指令的值修改的时候触发，提供值变化后，dom 更新的逻辑
      update(el, binding) {
        console.log('指令的值修改了');
        el.style.color = binding.value
      }
    }
  }
}
</script>
```

---

## 五、自定义指令 — v-loading 指令封装

### 1、场景

实际开发过程中，发送请求需要时间，在请求的数据未回来时，页面会处于空白状态 → 用户体验不好。

### 2、需求

封装一个 `v-loading` 指令，实现加载中的效果。

### 3、分析

1. 本质 loading 效果就是一个蒙层，盖在了盒子上
2. 数据请求中，开启 loading 状态，添加蒙层
3. 数据请求完毕，关闭 loading 状态，移除蒙层

### 4、实现

1. 准备一个 loading 类，通过伪元素定位，设置宽高，实现蒙层
2. 开启关闭 loading 状态（添加移除蒙层），本质只需要添加移除类即可
3. 结合自定义指令的语法进行封装复用

### 5、代码示例

```html
<template>
  <div class="box" v-loading="isLoading">
    <ul>
      <li v-for="item in list" :key="item.id" class="news">
        <div class="left">
          <div class="title">{{item.title}}</div>
          <div class="info">
            <span>{{item.source}}</span>
            <span>{{item.time}}</span>
          </div>
        </div>
        <div class="right">
          <img :src="item.img" alt="">
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
// 安装 axios → yarn add axios
import axios from 'axios'
// 接口地址：http://hmajax.itheima.net/api/news
// 请求方式：get
export default {
  data() {
    return {
      list: [],
      isLoading: true
    }
  },
  async created() {
    // 1. 发送请求获取数据
    const res = await axios.get('http://hmajax.itheima.net/api/news')
    setTimeout(() => {
      // 2. 更新到 list 中，用于页面渲染 v-for
      this.list = res.data.data
      this.isLoading = false
    }, 2000)
  },
  directives: {
    loading: {
      inserted(el, binding) {
        binding.value ? el.classList.add('loading') : el.classList.remove('loading')
      },
      update(el, binding) {
        binding.value ? el.classList.add('loading') : el.classList.remove('loading')
      }
    }
  }
}
</script>

<style>
.box {
  width: 800px;
  min-height: 500px;
  border: 3px solid orange;
  border-radius: 5px;
  position: relative;
}
.news {
  display: flex;
  height: 120px;
  width: 600px;
  margin: 0 auto;
  padding: 20px 0;
  cursor: pointer;
}
.news .left {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding-right: 10px;
}
.loading::before {
  content: '';
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  /* ⚠️ 注意：需确保项目中存在 ./loading.gif 图片文件，否则蒙层无加载动画 */
  background: #fff url('./loading.gif') no-repeat center;
}
</style>
```

> **补充：** `v-loading` 指令在 Element UI 中有官方实现，实际项目中可直接使用 `v-loading="isLoading"`，无需自己封装。此外还支持 `element-loading-text`、`element-loading-spinner` 等修饰属性自定义加载文案和图标。

---

## 六、插槽 — 默认插槽

### 1、作用

让组件内部的一些结构支持自定义。

### 2、需求

要在页面中显示一个对话框，封装成一个组件。

### 3、问题

组件的内容部分，不希望写死，希望能使用的时候自定义。

### 4、语法

1. 组件内需要定制的结构部分，改用 `<slot></slot>` 占位
2. 使用组件时，`<MyDialog></MyDialog>` 标签内部，传入结构替换 slot

### 5、示例

**① 在 App.vue 中：**

```html
<template>
  <div>
    <MyDialog></MyDialog>
    <MyDialog>你确定要退出吗</MyDialog>
  </div>
</template>

<script>
import MyDialog from './components/MyDialog.vue'
export default {
  data() {
    return {}
  },
  components: {
    MyDialog
  }
}
</script>

<style>
body {
  background-color: #b3b3b3;
}
</style>
```

**② 在 MyDialog.vue 中：**

```html
<template>
  <div class="dialog">
    <div class="dialog-header">
      <h3>友情提示</h3>
      <span class="close">×</span>
    </div>
    <div class="dialog-content">
      <!-- 在要定制的位置使用 slot 占位 -->
      <slot></slot>
    </div>
    <div class="dialog-footer">
      <button>取消</button>
      <button>确认</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {}
  }
}
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
}
.dialog {
  width: 470px;
  height: 230px;
  padding: 0 25px;
  background-color: #ffffff;
  margin: 40px;
  border-radius: 5px;
}
.dialog-header {
  height: 70px;
  font-size: 20px;
  border-bottom: 1px solid #ccc;
  position: relative;
}
.dialog-header .close {
  position: absolute;
  right: 0px;
}
</style>
```

---

## 七、插槽 — 后备内容（默认值）

### 1、概念

封装组件时，可以为预留的 `<slot>` 插槽提供后备内容（默认内容）。

### 2、语法

在 `<slot>` 标签内，放置内容，作为默认显示内容。

### 3、效果

1. 外部使用组件时，不传东西，则 slot 会显示后备内容：

```html
<MyDialog></MyDialog>
```

2. 外部使用组件，传东西了，则 slot 整体会被换掉：

```html
<MyDialog>我是内容</MyDialog>
```

---

## 八、插槽 — 具名插槽

### 1、需求

一个组件内有多处结构，需要外部传入标签，进行定制。

### 2、语法

1. 多个 slot 使用 `name` 属性区分名字
2. `template` 配合 `v-slot:名字` 来分发对应标签
3. `v-slot:插槽名` 可简化成 `#插槽名`

### 3、示例

**MyDialog.vue 中定义：**

```html
<div class="dialog-header">
  <slot name="head"></slot>
</div>
<div class="dialog-content">
  <slot name="content"></slot>
</div>
<div class="dialog-footer">
  <slot name="footer"></slot>
</div>
```

**使用时：**

```html
<MyDialog>
  <template #head>
    大标题
  </template>
  <template #content>
    内容文本
  </template>
  <template #footer>
    <button>按钮</button>
  </template>
</MyDialog>
```

> **补充：** 如果一个组件中只有默认插槽没有具名插槽，使用时可以省略 `<template>`，直接把内容写在组件标签内部。但只要出现了具名插槽，所有插槽内容都必须用 `<template>` 包裹并指定插槽名。

---

## 九、插槽 — 作用域插槽

### 1、定义

slot 插槽的同时，是可以传值的。给插槽上可以绑定数据，将来使用组件时可以用。

### 2、场景：封装表格组件

1. 父传子，动态渲染表格内容
2. 利用默认插槽，定制操作列
3. 删除或查看都需要用到当前项的 id，属于组件内部的数据，通过作用域插槽传值绑定，进而使用

### 3、基本使用步骤

1. 给 slot 标签，以添加属性的方式传值：

```html
<slot :id="item.id" msg="测试文本"></slot>
```

2. 所有添加的属性，都会被收集到一个对象中：

```js
{ id: 3, msg: '测试文本' }
```

3. 在 template 中，通过 `#插槽名="obj"` 接收，默认插槽名为 default：

```html
<MyTable :list="list">
  <template #default="obj">
    <button @click="del(obj.id)">删除</button>
  </template>
</MyTable>
```

### 4、示例

**① 在 App.vue 中：**

```html
<template>
  <div>
    <MyTable :data="list">
      <template #default="obj">
        <button @click="del(obj.row.id)">删除</button>
      </template>
    </MyTable>
    <MyTable :data="list2">
      <template #default="obj">
        <button @click="show(obj.row)">查看</button>
      </template>
    </MyTable>
  </div>
</template>

<script>
import MyTable from './components/MyTable.vue'
export default {
  data() {
    return {
      list: [
        {id: 1, name: '张小花', age: 18},
        {id: 2, name: '孙大明', age: 19},
        {id: 3, name: '刘大忠', age: 17}
      ],
      list2: [
        {id: 1, name: '赵小云', age: 18},
        {id: 2, name: '刘一一', age: 19},
        {id: 3, name: '肖林', age: 17}
      ]
    }
  },
  methods: {
    del(id) {
      this.list = this.list.filter(item => item.id !== id)
    },
    show(row) {
      alert('姓名：' + row.name + '，年龄' + row.age)
    }
  },
  components: {
    MyTable
  }
}
</script>
```

>  **补充：** 作用域插槽接收时可直接解构，更简洁：
> ```html
> <template #default="{ row }">
>   <button @click="del(row.id)">删除</button>
> </template>
> ```

**② 在 MyTable.vue 中：**

```html
<template>
  <table class="my-table">
    <thead>
      <tr>
        <th>序号</th>
        <th>姓名</th>
        <th>年龄</th>
        <th>操作</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(item, index) in data" :key="item.id">
        <td>{{index + 1}}</td>
        <td>{{item.name}}</td>
        <td>{{item.age}}</td>
        <td>
          <!-- 1. 给 slot 标签添加属性名 -->
          <slot :row="item" msg="测试文本"></slot>
          <!-- 2. 将所有属性，添加到对象中 -->
          <!--
            row: {id: 2, name: '孙大明', age: 19},
            msg: '测试文本'
          -->
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  // props: { data: Array } 是简写形式
  // 等价于完整写法：
  // props: {
  //   data: {
  //     type: Array
  //   }
  // }
  // 也可使用数组语法：props: ['data']
  props: {
    data: Array
  }
}
</script>

<style scoped>
</style>
```

> **补充：** Vue 3 中使用 `v-slot` 的方式与 Vue 2 一致，但 Vue 3 移除了 `slot` 和 `slot-scope` 这两个已废弃的语法。Vue 2.6 之前的旧写法 `slot="header"` 和 `slot-scope="scope"` 在 Vue 2.6+ 仍兼容但不推荐。

---

## 十、单页应用程序 & 路由介绍

### 1、单页 vs 多页对比

| 开发分类 | 实现方式 | 页面性能 | 开发效率 | 用户体验 | 学习成本 | 首屏加载 | SEO |
|---------|---------|---------|---------|---------|---------|---------|-----|
| 单页 | 一个 html 页面 | 按需更新，性能高 | 高 | 非常好 | 高 | 慢 | 差 |
| 多页 | 多个 html 页面 | 整页更新，性能低 | 中等 | 一般 | 中等 | 快 | 优 |

### 2、适用场景

- **单页面应用：** 系统类网站 / 内部网站 / 文档类网站 / 移动端站点
- **多页面应用：** 公司官网 / 电商类网站

### 3、路由的概念

要控制更新，首先就要明确：**访问路径和组件的对应关系！**

1. 路由是一种映射关系
2. 根据路由就能知道不同路径的，应该匹配渲染哪个组件

> **补充：** 单页应用 SEO 差的问题可通过 **SSR（服务端渲染）** 或 **预渲染（Prerender）** 解决，Vue 生态中常用 Nuxt.js 框架实现 SSR。

---

## 十一、路由的基本使用

### 1、VueRouter 的使用

**① 下载：** 下载 VueRouter 模块到当前工程，版本 3.6.5

```bash
yarn add vue-router@3.6.5
```

**② 引入**

```js
import VueRouter from 'vue-router'
```

**③ 安装注册**

```js
Vue.use(VueRouter)
```

**④ 创建路由对象**

```js
const router = new VueRouter()
```

**⑤ 注入：** 将路由对象注入到 new Vue 实例中，建立关联

```js
new Vue({
  render: h => h(App),
  router
}).$mount('#app')
```

### 2、2 个核心步骤

**① 创建需要的组件（views 目录），配置路由规则**

```js
import Find from './views/Find.vue'
import My from './views/My.vue'
import Friend from './views/Friend.vue'

const router = new VueRouter({
  routes: [
    {path: '/find', component: Find},
    {path: '/my', component: My},
    {path: '/friend', component: Friend}
  ]
})
```

**② 配置导航，配置路由出口（路径匹配的组件显示的位置）**

```html
<div class="footer_wrap">
  <a href="#/find">发现音乐</a>
  <a href="#/my">我的音乐</a>
  <a href="#/friend">朋友</a>
</div>
<div class="top">
  <router-view></router-view>
</div>
```

### 3、示例

**① 在 main.js 中：**

```js
import Vue from 'vue'
import App from './App.vue'
import VueRouter from 'vue-router'  // 引入
Vue.use(VueRouter)  // VueRouter 插件初始化

import Find from './views/Find.vue'
import My from './views/My.vue'
import Friend from './views/Friend.vue'

const router = new VueRouter({
  routes: [
    {path: '/find', component: Find},
    {path: '/my', component: My},
    {path: '/friend', component: Friend}
  ]
})

Vue.config.productionTip = false

new Vue({
  render: h => h(App),
  router
}).$mount('#app')
```

**② 在 App.vue 中：**

```html
<template>
  <div>
    <div class="footer_wrap">
      <a href="#/find">发现音乐</a>
      <a href="#/my">我的音乐</a>
      <a href="#/friend">朋友</a>
    </div>
    <div class="top">
      <router-view></router-view>
    </div>
  </div>
</template>

<script>
export default {}
</script>

<style scoped>
</style>
```

**③ 在 src 下新建 views 文件夹，再在 views 下新建 Find.vue、Friend.vue、My.vue：**

在 Find.vue 中：

```html
<template>
  <div>
    <p>发现音乐</p>
    <p>发现音乐</p>
  </div>
</template>

<script>
export default {
  name: 'FindMusic'
}
</script>

<style></style>
```

My.vue 与 Friend.vue 的写法相同，不同之处：

- 发现音乐 → 我的音乐 / My.vue
- 发现音乐 → 我的朋友 / Friend.vue

### 4、组件目录的存放

1. 组件分类有两类：**页面组件**和**复用组件**，便于维护
2. **页面组件** — views 文件夹 → 配合路由，页面展示
3. **复用组件** — components 文件夹 → 封装复用

>  **补充：** 使用 `<a href="#/find">` 这种方式是 hash 模式路由，URL 中会带 `#`。Vue Router 还支持 history 模式，通过 `new VueRouter({ mode: 'history', routes: [...] })` 开启，URL 更美观但需要后端配合配置。

---

## 十二、路由的封装抽离

### 1、目的

在 index.js 中将代码封装出来，可以拆分模块，利于维护。

### 2、示例

**① 在 src 下新建一个文件夹 router，再在 router 下新建 index.js 文件**

**② 在 main.js 中：**

```js
import Vue from 'vue'
import App from './App.vue'
import router from './router/index'

Vue.config.productionTip = false

new Vue({
  render: h => h(App),
  router
}).$mount('#app')
```

**③ 在 router/index.js 中：**

```js
// ..相当于@"不完全准确：
// `..` 是相对路径，表示上一级目录（从 router/ 回到 src/）
// `@` 是 webpack 别名，默认指向 src 目录
// 两者在 router/index.js 中效果相同，但概念不同
import Find from '../views/Find'
import My from '../views/My'
import Friend from '../views/Friend'

import Vue from 'vue'  // 要写上，因为 index.js 是独立模块，main.js 中的 import 不会自动共享过来
import VueRouter from 'vue-router'

Vue.use(VueRouter)

const router = new VueRouter({
  routes: [
    {path: '/find', component: Find},
    {path: '/my', component: My},
    {path: '/friend', component: Friend}
  ]
})

export default router
```

> **补充：** 如果项目配置了 `@` 别名（vue-cli 创建的项目默认已配置），可以写成 `import Find from '@/views/Find'`，这样无论文件在哪个目录层级都不用关心相对路径的 `../` 数量，更不容易出错。

---

## 十三、声明式导航 — 导航链接

### 1、需求

实现导航高亮效果。

### 2、vue-router 提供了一个全局组件 router-link（取代 a 标签）

1. **能跳转：** 配置 `to` 属性指定路径（必须），本质还是 a 标签，`to` 无需 `#`
2. **能高亮：** 默认就会提供高亮类名

### 3、示例

```html
<template>
  <div>
    <div class="footer_wrap">
      <router-link to="/find">发现音乐</router-link>
      <router-link to="/my">我的音乐</router-link>
      <router-link to="/friend">朋友</router-link>
    </div>
    <div class="top">
      <router-view></router-view>
    </div>
  </div>
</template>

<script>
export default {}
</script>

<style>
body {
  margin: 0;
  padding: 0;
}
.footer_wrap {
  position: relative;
  left: 0;
  top: 0;
  display: flex;
  width: 100%;
  text-align: center;
  background-color: #333;
  color: #ccc;
}
.footer_wrap a {
  flex: 1;
  text-decoration: none;
  padding: 20px 0;
  line-height: 20px;
  background-color: #333;
  color: #ccc;
  border: 1px solid black;
}
.footer_wrap a.router-link-active {
  background-color: purple;
}
.footer_wrap a:hover {
  background-color: #555;
}
</style>
```

> **补充：** `router-link` 还支持 `tag` 属性指定渲染成什么标签（Vue 2 中），如 `<router-link to="/find" tag="li">` 会渲染成 `<li>` 标签。但 Vue 3 中已移除 `tag` 属性，改用 `<router-link>` 的默认插槽或作用域插槽方式自定义。

---

## 十四、声明式导航 — 两个高亮类名

### 1、router-link 自动给当前导航添加了 2 个高亮类名

1. `router-link-exact-active`
2. `router-link-active`

### 2、两个类名的区别

**① `router-link-active` — 模糊匹配（用的多）**

`to="/my"` 可以匹配 `/my`、`/my/a`、`/my/b` ...（以 /my 开头的路径都会匹配）

**② `router-link-exact-active` — 精确匹配**

`to="/my"` 仅可以匹配 `/my`

> **补充：** 可以通过 `linkActiveClass` 和 `linkExactActiveClass` 配置项自定义高亮类名：
> ```js
> const router = new VueRouter({
>   linkActiveClass: 'active',        // 自定义模糊匹配类名
>   linkExactActiveClass: 'exact-active',  // 自定义精确匹配类名
>   routes: [...]
> })
> ```
> 这样在 CSS 中就可以直接写 `.active { ... }` 而不用写长长的 `.router-link-active`。

