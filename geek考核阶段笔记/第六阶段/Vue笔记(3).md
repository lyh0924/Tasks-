- [Vue 组件通信学习笔记](#vue-组件通信学习笔记)
  - [一、data 是一个函数](#一data-是一个函数)
    - [1. 为什么组件的 data 必须是函数](#1-为什么组件的-data-必须是函数)
    - [2. 例子：BaseCount 计数器组件](#2-例子basecount-计数器组件)
      - [在 BaseCount.vue 中：](#在-basecountvue-中)
      - [在 App.vue 中：](#在-appvue-中)
  - [二、组件通信](#二组件通信)
    - [1. 什么是组件通信](#1-什么是组件通信)
    - [2. 不同组件关系](#2-不同组件关系)
    - [3. 组件通信解决方案](#3-组件通信解决方案)
    - [4. 父子通信流程图](#4-父子通信流程图)
  - [三、props 父传子](#三props-父传子)
    - [示例代码：（父传子）](#示例代码父传子)
      - [在 App.vue 中：](#在-appvue-中-1)
      - [在 Son.vue 中：](#在-sonvue-中)
  - [四、$emit 子传父](#四emit-子传父)
    - [示例代码：（子传父）](#示例代码子传父)
      - [在 App.vue 中：](#在-appvue-中-2)
      - [在 Son.vue 中：](#在-sonvue-中-1)
  - [五、Prop 详解](#五prop-详解)
    - [1. Prop 定义](#1-prop-定义)
    - [2. Prop 作用](#2-prop-作用)
    - [3. 特点](#3-特点)
    - [示例：传递多个不同类型的 prop（UserInfo 组件）](#示例传递多个不同类型的-propuserinfo-组件)
      - [在 App.vue 中：](#在-appvue-中-3)
      - [在 UserInfo.vue 中：](#在-userinfovue-中)
  - [六、props 校验](#六props-校验)
    - [1. 作用](#1-作用)
    - [2. 语法](#2-语法)
    - [3. 类型校验（最常用）](#3-类型校验最常用)
    - [示例：进度条组件 BaseProgress](#示例进度条组件-baseprogress)
      - [在 App.vue 中：](#在-appvue-中-4)
      - [在 BaseProgress.vue 中：](#在-baseprogressvue-中)
    - [4. props 校验完整写法](#4-props-校验完整写法)
    - [在类型校验的代码基础上进行修改：](#在类型校验的代码基础上进行修改)
  - [七、Prop \& data、单向数据流](#七prop--data单向数据流)
    - [1. 共同点](#1-共同点)
    - [2. 区别](#2-区别)
    - [3. 示例：计数器组件的正确写法](#3-示例计数器组件的正确写法)
      - [错误写法（直接改 props）：](#错误写法直接改-props)
      - [正确写法（通过 $emit 通知父组件改）：](#正确写法通过-emit-通知父组件改)
        - [① 在 BaseCount.vue 中：](#-在-basecountvue-中)
        - [② 在 App.vue 中：](#-在-appvue-中)
  - [八、v-model 详解](#八v-model-详解)
    - [1. 原理](#1-原理)
    - [2. v-model 简化组件代码](#2-v-model-简化组件代码)
  - [表单类组件封装](#表单类组件封装)
    - [表单类组件封装](#表单类组件封装-1)
    - [应用实例：BaseSelect 下拉选择组件](#应用实例baseselect-下拉选择组件)
      - [在 App.vue 中：](#在-appvue-中-5)
      - [在 BaseSelect.vue 中：](#在-baseselectvue-中)
  - [九、.sync 修饰符](#九sync-修饰符)
    - [1. 作用](#1-作用-1)
    - [2. 特点](#2-特点)
    - [3. 场景](#3-场景)
    - [4. 本质](#4-本质)
    - [示例：BaseDialog 弹框组件](#示例basedialog-弹框组件)
      - [在 App.vue 中：](#在-appvue-中-6)
      - [在 BaseDialog.vue 中：](#在-basedialogvue-中)
  - [组件通信方案总结](#组件通信方案总结)
# Vue 组件通信学习笔记

---

## 一、data 是一个函数

### 1. 为什么组件的 data 必须是函数
一个组件的 **data 选项必须是一个函数** → 保证每个组件实例，维护独立的一份数据对象。

每次创建新的组件实例，都会新执行一次 data 函数，得到一个新对象。

> **补充**：如果 data 是一个对象的话，所有组件实例会共享同一份数据，一个实例改了数据，其他所有实例都会跟着变。用函数的话，每次调用都返回一个全新的对象，各组件实例的数据互不影响。

---

### 2. 例子：BaseCount 计数器组件

#### 在 BaseCount.vue 中：
```vue
<template>
  <div class="base-count">
    <button @click="count--">-</button>
    <span>{{ count }}</span>
    <button @click="count++">+</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      count: 999
    }
  }
}
</script>

<style scoped>
.base-count {
  margin: 20px;
}
</style>
```

#### 在 App.vue 中：
```vue
<template>
  <div id="app">
    <BaseCount></BaseCount>
    <BaseCount></BaseCount>
  </div>
</template>

<script>
import BaseCount from './components/BaseCount.vue'

export default {
  name: 'App',
  components: {
    BaseCount
  }
}
</script>
```

>  **理解**：页面上放了两个 BaseCount 组件，因为 data 是函数，每个计数器都有自己独立的 count，点击第一个的 + 号不会影响第二个。

---

## 二、组件通信

### 1. 什么是组件通信
组件通信，就是指**组件与组件之间的数据传递**。

① 组件的数据是独立的，无法直接访问其他组件的数据
② 想用其他组件的数据 → 组件通信

---

### 2. 不同组件关系
组件关系分类：
- ① **父子关系**
- ② **非父子关系**（兄弟关系、跨层级关系等）

```
      A
     / \
    B   C
```

A 分别与 B 和 C 是**父子关系**，B 和 C 是**非父子关系**（兄弟关系）。

---

### 3. 组件通信解决方案

| 关系 | 方案 |
|------|------|
| 父子关系 | `props` 和 `$emit` |
| 非父子关系 | a. `provide & inject`  b. `event bus` |
| 通用解决方案 | `Vuex`（适合复杂业务场景） |

> **补充**：
> - Vue 3 中 event bus 已经不推荐了，官方推荐用第三方库 `mitt` 来代替。
> - provide/inject 可以跨多层级传递数据，俗称"祖宗传后代"。
> - Vuex / Pinia 是状态管理库，适合大型项目中全局共享的数据。

---

### 4. 父子通信流程图

```
         父组件
     ┌───────────┐
     │  data数据  │
     │     ↓     │
props│           │$emit
     │     ↑     │
     │  子组件    │
     └───────────┘
```

① **父组件通过 props 将数据传递给子组件**（父 → 子，向下传）
② **子组件利用 $emit 通知父组件修改更新**（子 → 父，向上通知）

**props 流程**：
① 父中给子添加属性值
② 子 props 接收
③ 使用

**$emit 流程**：
① 子 $emit 发送消息
② 父中给子添加消息监听
③ 父中实现处理函数

---

## 三、props 父传子

### 示例代码：（父传子）

#### 在 App.vue 中：
```vue
<template>
  <div style="border:3px solid #000; margin:10px;">
    我是App组件
    <!-- 1. 给组件标签，添加属性的方式，传值 -->
    <Son :title="myTitle"></Son>
  </div>
</template>

<script>
import Son from './components/Son.vue'

export default {
  data() {
    return {
      myTitle: '你好'
    }
  },
  components: {
    Son
  }
}
</script>

<style>
</style>
```

#### 在 Son.vue 中：
```vue
<template>
  <div style="border:3px solid #000;margin:10px;">
    <!-- 3. 渲染使用 -->
    我是Son组件 {{ title }}
  </div>
</template>

<script>
export default {
  // 2. 通过 props 进行接收
  props: ['title']
}
</script>

<style>
</style>
```

> **补充**：
> - props 命名规范：在**模板（HTML）**中推荐用 **kebab-case**（短横线），在 **JS** 中用 **camelCase**（小驼峰）。
> - 比如模板里写 `:my-title="msg"`，JS 里接收 `props: ['myTitle']`，Vue 会自动转换。

---

## 四、$emit 子传父

### 示例代码：（子传父）
在父传子的代码基础上添加：

#### 在 App.vue 中：
```vue
<template>
  <div style="border:3px solid #000; margin:10px;">
    我是App组件
    <!-- 2. 父组件，对消息进行监听 -->
    <Son :title="myTitle" @changeTitle="handleChange"></Son>
  </div>
</template>

<script>
import Son from './components/Son.vue'

export default {
  data() {
    return {
      myTitle: '你好'
    }
  },
  methods: {
    // 3. 提供处理函数，提供逻辑
    handleChange(newTitle) {
      this.myTitle = newTitle
    }
  },
  components: {
    Son
  }
}
</script>
```

#### 在 Son.vue 中：
```vue
<template>
  <div style="border:3px solid #000;margin:10px;">
    我是Son组件 {{ title }}
    <button @click="changeFn">修改title</button>
  </div>
</template>

<script>
export default {
  props: ['title'],
  methods: {
    changeFn() {
      // 1. 通过 $emit，向父组件发送消息，通知
      this.$emit('changeTitle', 'Hello')
    }
  }
}
</script>
```

> **补充**：
> - `$emit` 第一个参数是**自定义事件名**，第二个参数是要传给父组件的数据（可以传多个，用逗号隔开）。
> - 父组件用 `@事件名` 监听，处理函数的参数就是子组件传过来的数据。
> - 子组件不能直接修改父组件传过来的 props，必须通过 $emit 通知父组件自己改，这就是**单向数据流**。

---

## 五、Prop 详解

### 1. Prop 定义
组件上注册的一些**自定义属性**。

### 2. Prop 作用
向子组件传递数据。

### 3. 特点
可以传递**任意数量、任意类型**的 prop。

> **补充**：prop 可以传字符串、数字、布尔值、数组、对象、函数等等，什么类型都能传。

---

### 示例：传递多个不同类型的 prop（UserInfo 组件）

#### 在 App.vue 中：
```vue
<UserInfo
  :username="username"
  :age="age"
  :isSingle="isSingle"
  :car="car"
  :hobby="hobby"
></UserInfo>
```

```vue
<script>
import UserInfo from './components/UserInfo.vue'

export default {
  data() {
    return {
      username: '小帅',
      age: 28,
      isSingle: true,
      car: {
        brand: '宝马'
      },
      hobby: ['篮球', '足球', '排球']
    }
  },
  components: {
    UserInfo
  }
}
</script>
```

#### 在 UserInfo.vue 中：
```vue
<template>
  <div class="userinfo">
    <h3>我是个信息组件</h3>
    <div>姓名：{{ username }}</div>
    <div>年纪：{{ age }}</div>
    <div>是否单身：{{ isSingle ? '是' : '否' }}</div>
    <div>座驾：{{ car.brand }}</div>
    <div>兴趣爱好：{{ hobby.join('、') }}</div>
  </div>
</template>

<script>
export default {
  props: ['username', 'age', 'isSingle', 'car', 'hobby']
}
</script>

<style scoped>
.userinfo {
  width: 300px;
  border: 3px solid #000;
  padding: 20px;
}
.userinfo > div {
  margin: 8px 0;
}
</style>
```

> **补充**：数组的 `join('、')` 方法可以把数组元素用指定符号拼接成字符串，比直接 `{{ hobby }}` 输出好看。

---

## 六、props 校验

### 1. 作用
为组件的 prop 指定验证要求，不符合要求，控制台就会有错误提示 → 帮助开发者快速发现错误。

### 2. 语法
① **类型校验**
② **非空校验**（required）
③ **默认值**（default）
④ **自定义校验**（validator）

---

### 3. 类型校验（最常用）

**语法**：
```js
props: {
  校验的属性名: 类型  // Number  String  Boolean  Array  Object ...
}
```

> **补充**：类型可以是 `String`、`Number`、`Boolean`、`Array`、`Object`、`Date`、`Function`、`Symbol` 等，也可以是自定义的构造函数。

---

### 示例：进度条组件 BaseProgress

#### 在 App.vue 中：
```vue
<template>
  <div id="app">
    <BaseProgress :w="width"></BaseProgress>
  </div>
</template>

<script>
import BaseProgress from './components/BaseProgress.vue'

export default {
  data() {
    return {
      width: 30
    }
  },
  components: {
    BaseProgress
  }
}
</script>
```

#### 在 BaseProgress.vue 中：
```vue
<template>
  <div class="base-progress">
    <div class="inner" :style="{ width: w + '%' }">
      <span>{{ w }}%</span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    w: Number
  }
}
</script>

<style scoped>
.base-progress {
  height: 26px;
  width: 400px;
  border-radius: 15px;
  background-color: #272425;
  border: 3px solid #f7f7f7;
  box-sizing: border-box;
}
.inner {
  height: 100%;
  border-radius: 15px;
  background-color: #42b983;
  color: #fff;
  text-align: center;
  line-height: 26px;
}
</style>
```

---

### 4. props 校验完整写法

**格式**：
```js
props: {
  校验的属性名: {
    type: 类型,
    required: true,      // 非空校验
    default: 默认值,      // 默认值
    validator(value) {
      // 自定义校验逻辑
      return 是否通过校验
    }
  }
}
```


---

### 在类型校验的代码基础上进行修改：

```js
props: {
  w: {
    type: Number,
    // required: true,
    default: 0,
    validator(value) {
      if (value >= 0 && value <= 100) {
        return true
      } else {
        console.error('传入的 prop w，必须是 0-100 的数字')
        return false
      }
    }
  }
}
```

> **补充**：
> - `default` 和 `required` 一般不同时用，有默认值就没必要非空了。
> - 如果 prop 类型是 **Array 或 Object**，`default` 必须是一个**函数**，返回默认值：
>   ```js
>   default: function() {
>     return []  // 或 {}
>   }
>   ```
>   原因和 data 必须是函数一样，避免多个实例共享同一份引用类型数据。
> - `validator` 函数返回 `true` 表示校验通过，返回 `false` 控制台会报警告。

---

## 七、Prop & data、单向数据流

> **单向数据流** → 父组件的 prop 更新，会单向向下流动，影响子组件。

### 1. 共同点
都可以给组件提供数据。

### 2. 区别
① **data 的数据是自己的** → 随便改
② **prop 的数据是外部的** → 不能直接改，要遵循单向数据流

> **补充**：单向数据流是 Vue 的核心设计理念之一。父级 prop 的更新会向下流动到子组件中，但反过来不行。这样可以防止子组件意外修改父组件的状态，导致数据流向难以理解。

---

### 3. 示例：计数器组件的正确写法

#### 错误写法（直接改 props）：
子组件直接 `count++` / `count--`，但 count 是父组件传过来的 prop，不能直接改。

#### 正确写法（通过 $emit 通知父组件改）：

##### ① 在 BaseCount.vue 中：

```vue
<template>
  <div class="base-count">
    <button @click="handleSub">-</button>
    <span>{{ count }}</span>
    <button @click="handleAdd">+</button>
  </div>
</template>

<script>
export default {
  // 2、props 传过来的数据（外部的数据，不能直接改）
  props: {
    count: Number
  },
  methods: {
    handleAdd() {
      // 子传父 this.$emit(事件名, 数据)
      this.$emit('changeCount', this.count + 1)
    },
    handleSub() {
      this.$emit('changeCount', this.count - 1)
    }
  }
}
</script>

<style scoped>
.base-count {
  display: flex;
  align-items: center;
  gap: 12px;
  font-size: 22px;
}
.base-count button {
  width: 40px;
  height: 40px;
  font-size: 24px;
  border: none;
  background: #42b983;
  color: white;
  border-radius: 6px;
  cursor: pointer;
}
.base-count span {
  min-width: 60px;
  text-align: center;
}
</style>
```

>  **理解**：自己的数据自己负责（谁的数据谁改）。count 是父组件的数据，所以得通知父组件去改，子组件不能直接动手。

##### ② 在 App.vue 中：

```vue
<template>
  <div id="app">
    <BaseCount @changeCount="handleChange" :count="count"></BaseCount>
  </div>
</template>

<script>
import BaseCount from './components/BaseCount.vue'

export default {
  data() {
    return {
      count: 666
    }
  },
  methods: {
    handleChange(newCount) {
      this.count = newCount
    }
  },
  components: {
    BaseCount
  }
}
</script>
```

---

## 八、v-model 详解

### 1. 原理
`v-model` 本质上是一个**语法糖**，例如应用在输入框上，就是 `value` 属性和 `input` 事件的合写。
1. 原理：v-model本质上是一个语法糖。例如应用在输入框上，就是value属性和input事件的合写
2. 作用：提供数据的双向绑定
    1. 数据变，视图跟着变 :value
    2. 视图变，数据跟着变 @input
3.  写法示例
```
<template>
  <div>
    <input v-model="msg1" type="text"><br><br>
    <!-- 模板中获取事件的形参->$event获取 -->
    <input :value="msg2" @input="msg2"=$event.target.value>
  </div>
</template>

<script>
export default{
    data(){
        return{
            msg1:'',
            msg2:''
        }
    }
}
</script>

<style></style>
```

> **补充**：
> ```html
> <input v-model="msg">
> ```
> 等价于：
> ```html
> <input :value="msg" @input="msg = $event.target.value">
> ```
> `$event` 就是事件对象，`$event.target.value` 就是输入框当前的值。

---

### 2. v-model 简化组件代码

父组件 v-model 简化代码，实现子组件和父组件数据**双向绑定**。

① **子组件中**：props 通过 `value` 接收，事件触发 `input`
② **父组件中**：`v-model` 给组件直接绑数据（`:value + @input` 的合写）

> **补充**：这是 Vue 2 中组件 v-model 的默认规则——默认用 `value` 这个 prop 名和 `input` 这个事件名。Vue 3 中改成了 `modelValue` 和 `update:modelValue`，注意区分版本。

---

## 表单类组件封装
### 表单类组件封装
1. 父传子:数据应该是父组件props传递过来的，v-model拆解绑定数据
2. 子传父:监听输入，子传父传值给父组件修改
3. 子组件不能使用v-model是因为，数据是父组件的。所以不能双向绑定
```
//在App.vue中：
<template>
  <div class="app">
    <BaseSelect :cityId="selectId" @changeId="selectId=$event">
    </BaseSelect>
  </div>
</template>
<script>
import BaseSelect from './components/BaseSelect.vue'
export default{
    data(){
        return{
          selectId:'103'
        }
    },
    components:{
        BaseSelect
    }
}
</script>


//在BaseSelect.vue中：
<template>
  <div>
    <select :value="cityId" @change="handleChange">
      <option value='101'>北京</option>
      <option value='102'>上海</option>
      <option value='103'>武汉</option>
      <option value='104'>深圳</option>
      <option value='105'>广州</option>
    </select>
  </div>
</template>

<script>
export default{
props:{
    cityId:string
},
methods:{
    handleChange(e){
        this.$emit('changeId',e.target.value)
    }
}
}
</script>
```

### 应用实例：BaseSelect 下拉选择组件

#### 在 App.vue 中：
```vue
<template>
  <div class="app">
    <!-- v-model => :value + @input -->
    <BaseSelect v-model="selectId"></BaseSelect>
  </div>
</template>

<script>
import BaseSelect from './components/BaseSelect.vue'

export default {
  data() {
    return {
      selectId: '103'
    }
  },
  components: {
    BaseSelect
  }
}
</script>

<style>
</style>
```

#### 在 BaseSelect.vue 中：
```vue
<template>
  <div>
    <select :value="value" @change="handleChange">
      <option value="101">北京</option>
      <option value="102">上海</option>
      <option value="103">武汉</option>
      <option value="104">深圳</option>
      <option value="105">广州</option>
    </select>
  </div>
</template>

<script>
export default {
  props: {
    value: String
  },
  methods: {
    handleChange(e) {
      this.$emit('input', e.target.value)
    }
  }
}
</script>
```

> **补充**：
> - select 标签的默认事件是 `change`（不是 input），所以子组件里监听的是 `@change`。
> - 但触发的事件名必须是 `input`，因为父组件用的是 `v-model`，默认监听 `input` 事件。
> - `e.target.value` 就是 select 当前选中的 option 的 value 值。

---

## 九、.sync 修饰符

### 1. 作用
可以实现子组件与父组件数据的**双向绑定**，简化代码。

### 2. 特点
prop 属性名，可以自定义，**非固定为 value**。

### 3. 场景
封装弹框类的基础组件，`visible` 属性，`true` 显示，`false` 隐藏。

### 4. 本质
就是 `.属性名.sync` → `:属性名 + @update:属性名` 的合写。

> **补充**：
> - v-model 默认用 value + input，适合表单类组件（输入框、下拉框等）。
> - .sync 可以自定义属性名，适合非表单类的双向绑定场景（比如弹框的显示隐藏、抽屉的开关等）。
> - **注意**：.sync 是 Vue 2 的语法，**Vue 3 中已经移除了 .sync**，统一用 `v-model:属性名` 的方式来实现同样的效果。

---

### 示例：BaseDialog 弹框组件

#### 在 App.vue 中：
```vue
<template>
  <div class="app">
    <button class="logout" @click="isShow = true">退出按钮</button>
    <!-- :visible.sync => :visible + @update:visible -->
    <BaseDialog :visible.sync="isShow"></BaseDialog>
  </div>
</template>

<script>
import BaseDialog from './components/BaseDialog.vue'

export default {
  data() {
    return {
      isShow: false
    }
  },
  components: {
    BaseDialog
  }
}
</script>
```

#### 在 BaseDialog.vue 中：
```vue
<template>
  <div v-show="visible" class="base-dialog-mask">
    <div class="title">
      <h3>温馨提示：</h3>
      <button @click="close" class="close">×</button>
    </div>
    <div class="content">
      <p>你确认要退出系统吗？</p>
    </div>
    <div class="footer">
      <button>确认</button>
      <button>取消</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    visible: Boolean
  },
  methods: {
    close() {
      this.$emit('update:visible', false)
    }
  }
}
</script>

<style scoped>
.base-dialog-mask {
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
}
</style>
```


>  **补充**：
> - `position: fixed` 是固定定位，相对于浏览器窗口定位，所以弹框遮罩能铺满整个屏幕。
> - `left: 0; top: 0; width: 100%; height: 100%;` 这四个属性配合 fixed，让遮罩层覆盖整个视口。
> - 子组件通过 `$emit('update:visible', false)` 通知父组件把 visible 改成 false，父组件因为用了 `.sync` 修饰符，会自动接收并更新。

---

## 组件通信方案总结

| 方案 | 方向 | 适用场景 | 关键语法 |
|------|------|----------|----------|
| props | 父 → 子 | 父子传数据 | `props: ['xxx']` |
| $emit | 子 → 父 | 子通知父改数据 | `this.$emit('事件名', 数据)` |
| v-model | 双向 | 表单类组件双向绑定 | `v-model="xxx"`（value + input） |
| .sync | 双向 | 非表单类双向绑定（如弹框） | `:xxx.sync="yyy"`（:xxx + @update:xxx） |
| provide/inject | 祖先 → 后代 | 跨多层级传数据 | `provide()` / `inject` |
| event bus | 任意 | 非父子组件通信 | `$on` / `$emit` |
| Vuex/Pinia | 全局 | 大型项目全局状态管理 | state / mutations / actions |
