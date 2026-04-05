# CSS学习笔记
## CSS分类
1. **内联样式表（行内样式表）**：样式写到标签内部，可以控制**当前标签样式**，特殊情况使用
`<p style="color:red;">文字内容</p>`
2. **内部样式表**：写到`<head>`标签中，脱离结构，可控制**当前页面所有标签**，较常用,如：
```
<head>
 <style>
  div{
       color:red;
     }
 </style>
</head＞  
<body>
     <div>红色</div＞
</body>
```

3. **外部样式表**：单独新建一个css文件，完全脱离结构，可控制**整个网站所有标签**，最常用
`<link rel="stylesheet" href="./css/index.css">`写在html文件中的`<head>`中
此时在html文件中要改变以下颜色
`<div>蓝色</div>`
则在**新建的css文件夹**中找到要进行书写的**index.css文件**，在里面书写  
```
div{
    color:blue;
    }
```   
## 基础选择器
1. **类型选择器**
   1. 选择某个类型的元素，也称标签选择器
如：div { //选择所有div标签.
color:gold;
}

    span { //选择所有span标签修改样式
color:green;
}

    2. **css层叠性**：css规则可以同时作用于一个元素，层叠性解决了样式冲突问题，后定义的样式覆盖了先前样式.

    3. **书写规范**：
   * 选择器和大括号中间以及属性名和属性值中间(:和文字中间)要保留1个空格距离.
   * 每css属性独占一行
    4. **注释快捷键**：crtl+/ (注释内容在左右两侧保持一个空格距离)
2. **类选择器**
    1. 可选择某1个元素或多个元素
    2. 语法  
**css(.类名{样式声明；…})**  
```
<style>
.Pink{
color:Pink;
}
.sub-nav{
    font-size:20px;
}
</style>  
```
**html(<标签 class="类名">)**
```
<body>
<div class="Pink">春</div>
<div>夏</div>
<div>秋</div>
<div class="Pink sub-nav">冬</div>
</body>
```  


 **注意**：
*  类名自定义，不能是中文、纯数字    
*   多个英文单词组成尽量使用-链接
* 命名有要意义，尽量见名知义
*  class属性可以有多类名中间用空格隔开
*  类选择器的权重(优先级)高于类型选择器(标签选择器)
3. **id选择器**
    1. 选择HTML中具有特定id属性的唯一元素
    2. 语法
**css(#id名{样式声明；…})**
#header{
color:red;
}
**html（<标签 id="id名”>)**
`<div id="header">修改样式</div>`
    3. **id选择器和类选择器的区别**
**类选择器**
语法：以.开头，后跟类名（如.nav）
作用：选择class属性的一个或多个元素
特点：可以使用多次
类似：身份证的名字，可以使用多次
场景：后期修改样式基本都是类选择器

        **id选择器**
语法：以#开头，后跟id名（如#header）
作用：选择 特定id属性的唯一元素
特点：同一页面中，id值必须唯一（不能重复）
类似：身份证的编号，唯一，只能用一次
场景：后期主要是配合JavaScript添加交互效果  
## 字体样式  
### 字体颜色  
1. **关键字**：这些颜色通常不会在生产环境的网站中使用，主要学习使用，比如，red,green,blue,pink
   如：`p {color:pink;}`    
   ```  
   css
   .pink {
    color:pink;
   }
   html
   <p class="pink">字体颜色可以使用颜色名称设置</p>  
   ```
2. **十六进制**：开发通常使用这个，比如：#FF0000或者#F00
   如：`p {color:#F00;}`   
   ```
   css
   .color16 {
       color: #F00;
   }  
   html  
   <p class="color16">字体颜色可以使用十六进制颜色值设置</p> 
   ```
    
3. **rgb格式**：rgb（）函数接收三个函数，分别表示颜色的红，绿，蓝。比如：红色rgb(255,0,0) 
   `p {color:rgb(255,0,0)}` 
   ```
   css
   .rgb{
        color:rgb(255,0,0);
   }
   html
   <p class="rgb">字体颜色可以使用rgb或rgba设置</p>
   ```
4. **rgba格式**：rgba（255,0,0,0.3）文字透明，最后一个数值取0-1，0完全透明，1完全不透明
   ```
   css
   .rgba{
    color:rgba(255,0,0,0.3)
   }
   html
   <p class="rgba">文字可以半透明</p>  
   ``` 
### 字体族  
1. 给定一个有先后顺序的，由字体名或者字体族名组成的列表来选定的元素设置字体，属性值用逗号隔开，浏览器会选择列表中第一个该计算机上有安装的字体,网页开发一般使用无衬线字体
   ```
   body{
       font-family:Arial,Helvetica,snas-serif;
   }
   ``` 
如：  
```  
css
.font{
    font-family:黑体；
}
html
<p class="font">字体族可以使用字体名称设置</p>  
```  
### 字体大小  
1. 可以设置字体大小，像素px（css中用于定义长度，尺寸的单位）  
   ```
   css
   .p{
   font-size: 18px;
   }
   html  
   <p class="p">字体大小可以用px设置</p>  
   ```
### 字体风格  
1. font-style用来打开和关闭文本italic（斜体）  
2. 属性值：  
    1. normal：将文本设置为普通字体（将存在的斜体关闭）(通常用em或i标签取消默认倾斜)
    2. italic：如果当前字体的斜体版本可用，那么文本设置为斜体版本  
   ```  
   .italic<
   font-style:italic;/*设置斜体样式*/
   >
   em{
    font-style:normal;//让em取消斜体
   }  
   ```  
### 字体粗体   
1. 核心作用
 font-weight  用于设置文字的粗细大小。
2. 使用场景 
     1. 很多默认加粗的标题（如  `<h1> - <h6>` ），可以用CSS取消加粗
     2. 批量处理文字时，用CSS给指定内容统一加粗
 3. 属性值
-  normal ：正常粗细
-  bold ：加粗
其他值受父元素属性影响，基本不用
    数字属性值（常用）
-  400 ：正常粗细
-  700 ：加粗
取值范围为100~900之间的整百数，日常开发常用400和700
```
css
/* 取消加粗 */
.nobold{
  font-weight: normal;/* 或 font-weight: 400; */
}
/* 给正文加粗 */
bold {
  font-weight: bold;/* 或 font-weight: 700; */
}
html
<p class="bold">字体粗细可以使用数字</p>
<p class="nobold">字体粗细可以使用数字</p> 
```  
### text-decoration
1. 核心作用
  text-decoration用于设置或取消字体上的文本装饰。
2. 使用场景
1. 最常见用于设置/取消链接的下划线（比如去掉  `<a>`  标签默认的下划线）
2. 特殊场景下给文字添加删除线
3. 常用属性值
-  none ：取消所有文本装饰（常用于去掉链接默认下划线）
-  underline ：给文字添加下划线
-  overline ：给文字添加上划线
-  line-through ：给文字添加穿过文本的删除线
```
a {/* 去掉a标签默认下划线 */
  text-decoration: none;
}
p {/* 给文字加下划线 */
  text-decoration: underline;
}
.del-text {/* 给文字加删除线 */
  text-decoration: line-through;
}  
```  
## 文本布局  
### 文本对齐text-align   
1. 核心作用
 text-align  用于控制文本在它所在的块级盒子内的**水平对齐**方式。
2. 使用场景
   1. 让文本、图片在盒子内实现水平对齐
   2. 实现文章文字的两端对齐
3. 常用属性值
-  left ：文本左对齐（默认值）
-  right ：文本右对齐
-  center ：文本水平居中对齐
-  justify ：自动改变字间距，实现文本两端对齐
```
css
  
/* 文本居中对齐（常用于标题） */
h1 {
  text-align: center;
}
/* 文本两端对齐（常用于正文段落） */
p {
  text-align: justify;
}
/* 文本右对齐（常用于落款、日期） */
.footer {
  text-align: right;
}
```
### text-indent  首行缩进
1. 核心作用
 text-indent  用于设置块级元素中文本第一行前面空格（缩进）的长度。
2. 使用场景
    1. 实现段落首行缩进2个字的排版效果
    2. 配合字体大小，实现隐藏文字的logo效果
3. 属性值及说明
   单位：em（最常用）
 
- 说明：em是相对单位，以本元素的文字大小为基准
- 规则： 1em  等于当前元素的字体大小
- 特殊情况：若当前元素未设置字体大小，则继承父元素字体大小
4. 常见写法
 
- 实现首行缩进2个字： text-indent: 2em; （适配不同字体大小，自适应缩进）
 ```
/* 段落首行缩进2个字 */
p {
  text-indent: 2em;
}

/* 特殊场景：设置具体缩进值（较少用） */
.box {
  font-size: 16px;
  text-indent: 32px; /* 等价于 2em */
}
```  
### letter-spacing  字间距
1. 核心作用
 letter-spacing  用于设置文本中字符（字）之间的间距。
2. 使用场景
调整字与字之间的距离，优化阅读体验，提升页面美观度。
3. 属性值
- 取值为数字+单位（如 px、em 等），支持正负值
- 正值：增大字间距
- 负值：缩小字间距
-  0 ：默认无额外间距
```
/* 给段落增加2px字间距 */
p {
  letter-spacing: 2px;
}
/* 给标题增加0.1em字间距（相对单位，适配字体大小） */
h1 {
  letter-spacing: 0.1em;
}
/* 缩小字间距 */
.tight-text {
  letter-spacing: -1px;
}
```
### line-height 行高
1. 核心作用
设置文本每行之间的高度，控制文本行与行的上下间距。
2. 使用场景
1. 设置多行文本之间的上下间距，改善阅读体验
2. 实现单行文本在容器内的垂直居中
3. 属性值
1. 数字+px：固定行高，例如 line-height: 25px;
2. 数字不带单位：表示当前字体大小的倍数，是推荐用法，例如 line-height: 1.5;
4. **单行文本**垂直居中原理
行高由上间距、文本高度、下间距组成。**当行高等于盒子高度时**，上下间距会自动均等，从而实现单行文字垂直居中。
```
/* 多行文本使用1.5倍行高 */
p {
  line-height: 1.5;
}

/* 单行文本垂直居中（行高=盒子高度） */
.box {
  height: 40px;
  line-height: 40px;
}

/* 固定像素行高 */
.title {
  line-height: 30px;
}  
```  
## 盒子模型
1. **盒子模型组成**
CSS盒模型整体上适用于区块盒子，包含盒子内容、内边距、外边距、边框四部分。
    1. **盒子内容**：显示内容的区域，由内容或者指定宽度高度来决定内容大小。
    2. **内边距padding**：内容距离边框之间的距离。
    3. **边框 border**：边框盒子包住内容和内边距。
    4. **外边距 margin**：该盒子与其他元素之间的距离。 
### 盒子模型组成-边框基础
1. border 属性用于设置盒子边框,设置**盒子四条或者单独边框**
属性规则
**border: 边框粗细 边框样式 边框颜色;**
  - 边框由三部分属性值组成，中间必须用空格隔开
  - 三部分属性值没有先后顺序
如：  
```
/* 边框: 1像素 实线 颜色 */
border: 1px solid #f1f1f1;
```
2. **常用边框样式**
dotted：点状边框，由圆点组成的虚线
dashed：虚线边框，由短横线组成的虚线
solid：实线边框，单一线条
3. 不同边框样式代码实现
css
```
.box1 {/* 实线边框 */
  border: 1px solid red;
}
.box2 {/* 虚线边框 */
  border: 1px dashed red;
}
.box3 {/* 点线边框 */
  border: 1px dotted red;
}

html
<div class="box1">实线边框</div>
<div class="box2">虚线边框</div>
<div class="box3">点线边框</div>
```
### 盒子公共样式与HTML基础结构
```
html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>盒子模型-边框设置</title>
  <style>
    div[class*="box"] {/* 选中所有class名包含box的div元素，设置统一样式 */
      width: 200px;
      height: 200px;
      margin: 20px;
    }
  </style>
</head>
</html>
```
### 单边边框设置
1. border属性可单独设置某一条边的边框，方位名词对应：top（上）、bottom（下）、left（左）、right（右）
2. **使用场景**
* 实现四个边框不同的样式
* 用底部一条线做分割线
3. **单边边框属性**
``` 
css
border-top: 1px solid pink;
border-bottom: 1px solid pink;
border-left: 1px solid pink;
border-right: 1px solid pink;
```

4. **单边边框代码实现与层叠规则**
```
css
.box5 {  /* 先给所有边框设置统一样式 */
    border: 1px solid #d9e0ee;
  border-top: 3px solid #ff8400;  /* 再单独设置对应边，覆盖统一样式 */
}
```
**规则说明：当同时设置全局border和单边border属性时，单边属性会层叠覆盖全局border的对应边样式，实现单条边框的差异化设置。**  
### 圆角边框
1. border-radius 允许设置元素的外边框圆角
2. **属性语法**：border-radius: 属性值;
      **属性值支持数字+px或百分比**
```
css
.button {
     border-radius: 10px;
}
```
3. **正方形实现圆形效果**
```
css 
.radius1 {
  width: 100px;
  height: 100px;
  background-color: pink;
  border-radius: 50%;
}
```
**说明：正方形盒子设置border-radius为50%，即可实现圆形效果**

4. **矩形常规圆角实现**
```
css
.radius2 {
  width: 200px;
  height: 80px;
  background-color: pink;
  border-radius: 10px;
}
说明：给矩形盒子设置固定像素的border-radius，即可实现常规的圆角矩形效果
```
5. **胶囊按钮实现**
```
css
.radius3 {
  width: 200px;
  height: 40px;
  background-color: skyblue;
  border-radius: 20px;
}
.radius4 {
  width: 40px;
  height: 200px;
  background-color: skyblue;
  border-radius: 20px;
}
html
<div class="radius3">胶囊按钮</div>
<div class="radius4">胶囊按钮</div>
```
**胶囊按钮 实现规则：设置圆角为宽度或者高度较小值的一半**
  6. **圆角实现规则总结**
*  胶囊圆角：长方形设置圆角为宽度（或高度）**较小值的一半**
- 圆形：正方形设置圆角为**高度的一半**，或者直接设置为**50%**

7. **图片实现圆形效果**
```
css
.jia {
  border-radius: 50%;
}

html
<img src="./img/w1.webp" alt="" class="jia">
```
**给img标签设置border-radius:50%，即可将图片裁剪为圆形效果**
8. **多值圆角写法与规则**
**实现不规则圆角，圆角写法与对应作用**
* 记忆与**使用规则**：
  多个属性值之间用**空格**隔开
  不需要圆角的角，设置为**0**即可
  四个值按**顺时针顺序**，分别对应左上角、右上角、右下角、左下角的圆角大小，**数值越大对应角的圆角弧度越大**
 
- border-radius: 10px; **四个角统一设置为10px圆角**
- border-radius: 10px 20px; **左上、右下是10px，右上、左下是20px**
- border-radius: 10px 20px 30px; **左上是10px，右上、左下是20px，右下是30px**
- border-radius: 10px 20px 30px 40px; **左上10px，右上20px，右下30px，左下40px**
  
**通用语法：border-radius: 左上角 右上角 右下角 左下角;**
### 盒子模型-内边距
1. **内边距padding**位于边框和内容区域之间,有多个值用空格隔开，遵循顺时针记忆规则
2. **内边距写法与作用**
padding: 10px;  **上下左右4个内边距**都是10px
padding: 10px 20px;  **上下**内边距是10px，**左右**内边距是20px
padding: 10px 20px 30px;  **上**是10px，**左右**是20px，**下**是30px
padding: 10px 20px 30px 40px; **上**10px，**右**20px，**下**30px，**左**40px（顺时针顺序）
3. **单边内边距**设置（根据方位名词）：
* **padding-left**: 10px; → 左内边距
* **padding-right**: 10px; → 右内边距
* **padding-top**: 10px; → 上内边距
* **padding-bottom**: 10px; → 下内边距
### 盒子模型外边距-margin
1. 外边距（margin）多个值使用空格分隔,**遵循上右下左顺序**
2. **外边距写法及作用**：
* margin: 10px;  → 上下左右4个外边距都是10px
*  margin: 10px 20px;  → 上下外边距10px，左右外边距20px
*  margin: 10px 20px 30px;  → 上10px，左右20px，下30px
*  margin: 10px 20px 30px 40px;  → 上10px，右20px，下30px，左40px
3. **单边设置**：通过方位名词单独设置，如 margin-left: 10px; 、 margin-top: 10px; 
4. **注意事项**：
* 行内元素**左右外边距生效，上下外边距无效**
* 行内元素**设置宽度和高度也无效**
5. **块级盒子水平居中** 
1. **核心技巧**：块级元素可**利用 margin**实现水平居中
2. **实现条件**：  
* 块级盒子必须设置宽度
* 只需设置左右外边距为auto（简写： margin: 0 auto; ）
6. **外边距合并**（相邻兄弟元素） 
    1. **现象**：并列关系（兄弟）的块级元素，上下外边距会出现合并（折叠）,因此**只需设置其中一个盒子的外边距即可**，无需重复设置
    2. **规则**：合并后的外边距大小 = 两个单个外边距中的较大值。
    3. **示例代码：**
```
html
  
<style>
.boxA {
  width: 100px;
  height: 100px;
  background-color: pink;
  margin-bottom: 100px; /* 下外边距100px */
}
.boxB {
  width: 100px;
  height: 100px;
  background-color: pink;
  margin-top: 50px; /* 上外边距50px */
}
</style>
<!-- 最终间距为100px（取最大值） -->
```
7. **外边距塌陷（父子嵌套元素）**
    1. 现象：嵌套关系（父子）的块级元素，给子盒子设置上下外边距，会导致父盒子跟随移动（塌陷），破坏页面布局。
    2. 解决方案：
* 方案1：**给父盒子添加边框**（ border: 1px solid #000; ，父盒子本身有边框则无塌陷问题）
* 方案2：**给父盒子添加内边距**（ padding-top: 20px; ，需注意父盒子高度会增加对应内边距值）
* 方案3：**给父盒子添加 overflow: hidden;** （触发BFC，解决塌陷）

   **塌陷解决方案代码示例**
``` 
1. 方案1（加边框）：
 
css
  
.father {
  width: 150px;
  height: 150px;
  background-color: pink;
  border: 1px solid #000; /* 关键：添加边框 */
}
.son {
  width: 80px;
  height: 80px;
  background-color: purple;
  margin-top: 20px;
}
 
 
2. 方案2（加内边距）：
 
css
  
.father {
  width: 150px;
  height: 150px;
  background-color: pink;
  padding-top: 20px; /* 关键：添加上内边距 */
}
.son {
  width: 80px;
  height: 80px;
  background-color: purple;
  /* 子元素margin-top可移除，或保留不影响 */
}
 
 
3. 方案3（overflow:hidden）：
 
css
  
.father {
  width: 150px;
  height: 150px;
  background-color: pink;
  overflow: hidden; /* 关键：触发BFC */
  /* 可注释掉border和padding */
  /* border: 1px solid #000; */
  /* padding-top: 20px; */
}
.son {
  width: 80px;
  height: 80px;
  background-color: purple;
  margin-top: 20px;
}  
```
### 盒子模型默认尺寸规则
1. 在CSS盒子模型的默认定义中，除了width和height会决定盒子内容区大小外，padding（内边距）和border（边框）都会**额外撑大盒子的整体尺寸**，给页面布局的尺寸计算带来困扰。
2. **尺寸计算示例**：
* 仅设置 width: 200px ，无border和padding时，盒子实际宽度为200px
* 当设置 width: 200px 、 border: 5px 、 padding: 10px 时，盒子实际宽度 = 200 + 5*2 + 10*2 = 230px
3. **核心需求**：开发中常需要让盒子的最终总尺寸，始终等于设定的width/height值，不受border和padding的影响
4. **box-sizing属性的两种核心模式** 
   **box-sizing: content-box** （默认值，标准盒模型）
* 尺寸计算规则：盒子最终实际大小 = 设定的width/height + padding + border
* 示例： width: 140px  +  border: 10px solid red  +  padding: 20px ，盒子最终实际宽度为 140 + 10*2 + 20*2 = 200px
   **box-sizing: border-box** 
- 尺寸计算规则：盒子最终实际大小 = 设定的width/height，padding和border会在盒子内部挤压内容区，不会撑大盒子
- 示例： width: 200px  +  border: 10px solid red  +  padding: 20px ，盒子最终实际宽度仍为200px，内容区宽度自动缩小为 200 - 102 - 202 = 140px
5. 开发常用的全局盒模型**重置写法**
1. **通用重置方案**：使用通配符选择器 * ，给页面所有元素统一设置盒模型规则，是前端开发的常用初始化写法：
``` 
css
  
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
```
2. **作用**：全局统一将所有元素的盒模型设置为 border-box ，避免后续每个元素单独设置，同时清除元素默认的内外边距，统一布局基准。
3. 优先级说明：全局设置后，若单个元素需要使用默认的 content-box ，可单独给该元素设置 box-sizing: content-box ，会覆盖全局的设置。
### 盒子背景background
1. **background**属性用于设置元素背景相关属性，可控制背景颜色、背景图片、背景位置、背景重复方式等样式
2. **background系列子属性详解** 
1. **background-color**
 
- 作用：设置元素背景颜色
- 常用值：颜色名称、十六进制色值、RGB/RGBA、透明度相关写法
- 示例代码： background-color: #f0f0f0; 
 
2. **background-image**
 
- 作用：设置元素的背景图片
- 常用值：url(图片路径/图片地址)
- 示例代码： background-image: url(bg.png); 
 
3. **background-repeat**
 
- 作用：控制背景图片是否重复平铺
- 常用值：repeat（默认值，全方向重复平铺）、no-repeat（不重复）、repeat-x（仅水平方向重复）、repeat-y（仅垂直方向重复）
- 示例代码： background-repeat: no-repeat; 
 
4. **background-position**
 
- 作用：定位背景图片在元素内的位置
- 常用值：xy轴坐标（可使用方位名词如center top，或px、%等单位）
- 示例代码： background-position: center; 
- 图片位置是相对浏览器视口大小来说的
 
5. **background-size**
 
- 作用：调整背景图片的尺寸大小
- 常用值：auto（默认值）、cover（覆盖整个元素，图片可能被裁切）、contain（完整包含图片，元素可能出现留白），也可使用px、%单位设置具体尺寸
- 示例代码： background-size: cover; 或background-size: 300px;  可设置具体的px、%单位，只写一个值时，另一个值会等比例缩放
 
6. **background-attachment**
 
- 作用：设置背景是否随页面滚动
- 常用值：scroll（默认值，随页面滚动）、fixed（固定在视口，不随页面滚动）
- 示例代码： background-attachment: fixed; 
7. **背景基础属性代码示例**
```
css
  
.box {
  width: 400px;
  height: 400px;
  /* 背景颜色 */
  background-color: pink;
  /* 背景图片 */
  background-image: url(./img/ldh.png);
  /* 背景平铺控制 */
  background-repeat: no-repeat;
  /* 其他平铺写法参考 */
  /* background-repeat: repeat-x; */
  /* background-repeat: repeat-y; */
}
```
8. **背景位置background-position用法详解**
    1. **写法规则**： background-position: x轴坐标 y轴坐标; 
    2. **支持的写法类型**：
 
- **像素单位写法**： background-position: 50px 10px;  （x轴偏移50px，y轴偏移10px）
- **百分比写法**： background-position: 50% 50%;  （x轴、y轴都居中）
- **方位名词写法**：支持top、bottom、left、right、center，示例：
-  background-position: left top;  （左上）
-  background-position: right center;  （右中）
-  background-position: center center;  （完全居中，可简写为 background-position: center; ）**简写规则**：如果只写一个值，第二个值会默认设置为center
### 样式初始化
 
- 作用：消除不同浏览器自带的默认样式，让你的页面在所有浏览器里显示效果一致，是写页面第一步要做的事。
- 基础代码：
```
css
  
/* 清除所有元素默认的内外边距，统一盒模型 */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
/* 清除列表的默认圆点 */
ul, ol {
  list-style: none;
}
/* 清除链接的默认下划线 */
a {
  text-decoration: none;
}
/* 清除输入框、按钮的默认外框线 */
input, button {
  outline: none;
}
```
- 补充：如果是做大项目，直接用现成的 Normalize.css 文件就行，不用自己手写
### 背景渐变
 
- 作用：给盒子、文字加渐变颜色，让页面更好看、更吸引用户。
- 最常用的线性渐变（基础用法）：
写在 background 属性里，格式： linear-gradient(渐变方向, 开始颜色, 结束颜色) 
- 例子：
```
css
  
/* 给盒子加从左到右，粉色到紫色的渐变 */
.box {
  background: linear-gradient(to right, pink, purple);
}
```
 
- 渐变方向可以写 to right （从左到右）、 to bottom （从上到下，不写默认就是这个），也可以写角度比如 90deg （和to right效果一样）
### 盒子阴影 box-shadow
 
- 作用：给盒子加阴影，让元素看起来更立体；鼠标放上去加阴影，还能突出当前元素
- 格式：
 box-shadow: X轴偏移量 Y轴偏移量 模糊程度 阴影颜色; 
- 例子：
```
css
  
.box {
  /* 水平不偏移，垂直向下15px，模糊30px，半透明黑色阴影 */
  box-shadow: 0 15px 30px rgba(0,0,0,0.1);
}
```
 
- 注意：
- X偏移正数向右、负数向左；Y偏移正数向下、负数向上，0就是不偏移
- 模糊程度数值越大，阴影越柔和
- 用 rgba(0,0,0,0.1) 这种半透明颜色，阴影会更自然
## 过渡 transition
 
- 作用：让元素的样式变化（比如鼠标放上去变大、变色）不是瞬间跳变，而是平滑的动画效果，让页面更丝滑
- 基础的用法：
 **transition: 要变化的属性 过渡时间；**
可用**transition: all 0.3s;** 意思是所有属性变化，都有0.3秒的平滑过渡
- 重点：这个属性**一定要写在元素的默认样式里**，**不能只写在:hover里**
- 例子：
```

css
  
.box {
  width: 200px;
  height: 200px;
  background: pink;
  /* 过渡写在默认样式里，鼠标移入、移出都有动画 */
  transition: all 0.3s;
}
/* 鼠标放上去，盒子加阴影、放大1.1倍 */
.box:hover {
  box-shadow: 0 15px 30px rgba(0,0,0,0.1);
  transform: scale(1.1);
}
```
## 浮动
**1.浮动特性（float）**
   1.浮动元素会**脱离标准流(脱标)**,脱离标准普通流的控制（浮），移动到指定位置（动），俗称脱标,**脱标后将不再保留元素本来的位置**
   2.浮动的元素会**一行内显示**并且**元素顶部对齐**,**注意**：浮动的元素是互相贴靠在一起的（不会有默认缝隙），如果父级宽度装不下这些浮动的盒子，多出的盒子会自动另起一行对齐
   3.不管原先是什么显示模式的元素，添加浮动之后,浮动的元素会**具有行内块元素的特点**
   4.如果块级盒子没有设置宽度，默认宽度和父级一样宽；但是添加浮动后，它的宽度由内部的内容多少来决定
``` 
html
  
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>浮动的元素具有行内块元素特点</title>
  <style>
    /* 任何元素都可以浮动。不管原先是什么模式的元素，添加浮动之后具有行内块元素相似的特性。 */
    span,div {
      float: left;
      width: 200px;
      height: 100px;
      background-color: pink;
    }
    /* 如果行内元素有了浮动,则不需要转换块级/行内块元素就可以直接给高度和宽度 */
    p {
      float: right;
      height: 200px;
      background-color: purple;
    }
  </style>
</head>
<body>
  <span>1</span>
  <span>2</span>
</body>
</html>
```
5.网页布局通用策略（**网页布局第一准则**）：
先用标准流的父元素排列好页面的上下位置，再给父元素内部的子元素设置浮动，排列左右位置，以此约束浮动元素的范围，避免布局错乱
**两栏布局**
```
html
  
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>浮动元素搭配标准流父盒子</title>
  <style>
    /* 标准流父盒子，定宽居中，约束子元素 */
    .box {
      width: 1200px;
      height: 460px;
      background-color: pink;
      margin: 0 auto;
    }
    /* 左浮动子盒子 */
    .left {
      float: left;
      width: 230px;
      height: 460px;
      background-color: purple;
    }
    /* 左浮动子盒子，和左栏并排 */
    .right {
      float: left;
      width: 970px;
      height: 460px;
      background-color: skyblue;
    }
  </style>
</head>
<body>
  <div class="box">
    <div class="left">左侧</div>
    <div class="right">右侧</div>
  </div>
</body>
</html>
```
**商品列表布局**
```
html
  
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>浮动布局练习2</title>
  <style>
    /* 样式初始化 */
    * {
      margin: 0;
      padding: 0;
    }
    /* 清除列表默认圆点 */
    li {
      list-style: none;
    }
    /* 标准流父盒子，定宽居中 */
    .box {
      width: 1226px;
      height: 285px;
      background-color: pink;
      margin: 0 auto;
    }
    /* 浮动列表项，实现一行多列 */
    .box li {
      width: 296px;
      height: 285px;
      background-color: purple;
      float: left;
      margin-right: 14px;
    }
    /* 最后一项清除右边距，避免超出父盒子 */
    .box .last {
      margin-right: 0;
    }
  </style>
</head>
<body>
  <ul class="box">
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li class="last">4</li>
  </ul>
</body>
</html>
```
**左右分栏嵌套布局**
```
html
  
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>浮动布局练习3</title>
  <style>
    /* 标准流父盒子，定宽居中 */
    .box {
      width: 1226px;
      height: 615px;
      background-color: pink;
      margin: 0 auto;
    }
    /* 左栏左浮动 */
    .left {
      float: left;
      width: 234px;
      height: 615px;
      background-color: purple;
    }
    /* 右栏右浮动，内部可继续嵌套浮动布局 */
    .right {
      float: right;
      width: 992px;
      height: 615px;
      background-color: skyblue;
    }
  </style>
</head>
<body>
  <div class="box">
    <div class="left">左青龙</div>
    <div class="right">
      <div>1</div>
      <div>2</div>
      <div>3</div>
      <div>4</div>
      <div>5</div>
      <div>6</div>
      <div>7</div>
      <div>8</div>
    </div>
  </div>
</body>
</html>
```
## 定位  
1. 某个元素可以自由的在一个盒子内移动位置，并且压住其他盒子
2. 浮动可以让多个块级盒子一行没有缝隙排列显示，经常用于横向排列盒子
 

