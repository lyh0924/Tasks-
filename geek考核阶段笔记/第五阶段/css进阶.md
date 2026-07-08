- [Flex弹性盒布局](#flex弹性盒布局)
- [Grid 网格布局笔记](#grid-网格布局笔记)
  - [定义](#定义)
  - [网格容器](#网格容器)
  - [网格轨道(Grid Tracks)](#网格轨道grid-tracks)
  - [对齐方式](#对齐方式)
  - [做固定列的多行效果](#做固定列的多行效果)
  - [gap  属性 \&  repeat()  函数](#gap-属性--repeat-函数)
  - [auto-fit  自动填充完成响应式效果](#auto-fit-自动填充完成响应式效果)
  - [网格线](#网格线)
  - [网格填充方式](#网格填充方式)
- [媒体查询](#媒体查询)
- [object-fit  图片缩放](#object-fit-图片缩放)
- [CSS 书写顺序](#css-书写顺序)
- [CSS 鼠标样式（cursor 属性）](#css-鼠标样式cursor-属性)

# Flex弹性盒布局
1. **可以快速实现元素的对齐，分布和空间分配**
2. **核心**：
   1. 父盒子控制子盒子如何排列布局（亲父子）
   2. 父盒子称为容器，子盒子称为项目
   3. 主轴默认水平方向（向右），交叉轴默认垂直方向（向下），可以更改
3. **（容器）父盒子**：
   1. **display:flex**：可以让子盒子按照主轴方式排列
        1. 如果子元素有大小，则按照给定大小来显示
        2. 如果子元素没有大小，则高度拉伸充满父容器，宽度根据文字内容来决定
        3. 若子元素总宽度超过容器宽度，默认会压缩子元素
        4. 写在行内元素`<a>`标签中，可以给`<a>`直接设定高度和宽度了
    2. **justify-content**:定义主轴上的对齐方式
        1. flex-start:默认向左对齐
        2. flex-end：向右对齐
        3. center：居中
        4. space-around：每一个盒子的左右间隔（分配的空间）都是相同的
        5. space-between:首个子元素放到起点，末尾元素放置于终点
        6. space-evenly:每个子元素之间的间隔相等
    3. **align-items**:定义交叉轴上的对齐方式（**单行**时整体对齐）
        1. flex-start:项目在交叉轴起点对齐
        2. flex-end:项目在交叉轴终点对齐
        3. center:项目在交叉轴居中对齐
        4. stretch:项目拉伸填充整个容器高度（需**子项目无固定高度**）
        5. baseline:以项目的第一行文字对齐
    4. **flex-between**:定义主轴方向（改变主轴方向）
       1. row:默认值，子元素沿水平主轴（从左到右）排列
       2. row-reverse:子元素沿水平轴主轴反向排列（从右到左）
       3. column:子元素沿垂直主轴（从上到下）排列
       4. column-reverse:子元素沿垂直主轴反向排列（从下到上）
    5. **flex-wrap**:控制是否换行
       1. nowrap:不换行（全部横向排列，可能被压缩）
       2. wrap:换行
       3. wrap-reverse:行的顺序翻转
    6. **align-content**:定义多行时交叉轴上的对齐方式（仅当flex-wrap:wrap且内容换行的时候生效）（要给父盒子设定高度）（和justify-content用法相似）
        1. flex-start:上对齐
        2. flex-end：下对齐
        3. center：居中对齐
        4. space-around：每一个盒子的上下间隔（分配的空间）都是相同的
        5. space-between:首个子元素放到起点，末尾元素放置于终点，两端对齐
        6. space-evenly:每个子元素之间的间隔相等，项目间隔均匀分布
4. **项目（子盒子）属性**：子元素的属性用于控制自身的尺寸，顺序和对齐方式（属性写到小盒子处）
   1. **flex:1**:剩余空间占一份，并且可以伸缩盒子大小，数字表示剩余空间所占份数，是正整数。且flex的**优先级**高过width和height（有多少个小盒子就把父盒子分成几份，然后每个小盒子占一份）
        1. 此时若有四个盒子，一个盒子是flex:2,其余盒子是flex:1,则一个盒子占五分之二，其余盒子各占五分之一
        2. **flex:1和flex:2都是简写**：意味着**flex-grow**分别1和2（即定义子元素剩余空间分配**放大比例**。默认为0，即不放大）而**flex-shrink**（定义子元素剩余空间**缩小比例**。默认为1，空间不足时等比缩小，0为不缩小）,flex-basis（定义项目在主轴方向上的**初始大小**。默认为auto，优先级高于width height）
    2. **gap**:控制**子元素之间的空隙**，但是代码要写到**父盒子**上
        1. gap：20px;（行和列间距都是20像素）
        2. gap:20px 30px;(行间距是20像素，列间距是30像素)
# Grid 网格布局笔记 

## 定义
 
网格布局是一种二维布局模型（多行多列），允许开发者通过定义行和列来精确控制网页元素的位置和尺寸，还可以实现响应式设计。
 
## 网格容器
 
1. 给父盒子设置  display: grid; （块级-竖向排列）或者  display: inline-grid; （行内）
2. 与弹性盒子不同，在定义网格后，网页并不会马上发生变化。因为  display: grid;  的声明只创建了一个只有一列的网格
 
## 网格轨道(Grid Tracks)
1. 决定了网格容器的基础布局结构，为子元素提供放置的位置。
2. 绘制网格（网格轨道）
-  grid-template-columns ：定义网格中的列
-  grid-template-rows ：定义网格中的行
**属性值：**
- 有几个属性值，代表创建几列/几行
- 长度单位，比如  100px 
例子：
```
css
  
/* 定义三列，每列宽度为200px */
grid-template-columns: 200px 200px 200px;
/* 定义三行，每行高度为200px（保留空格） */
grid-template-rows: 200px 200px 200px;
```
3. 例子
```
css
  
/* CSS */
.box {
    display: grid;
    /* 创建列轨道 */
    grid-template-columns: 100px 100px 100px;
    width: 320px;
    /* 创建行轨道 */
    grid-template-rows: 100px 100px 100px;
    height: 320px;
    border: 1px solid red;
    margin: 20px;
}
.box div {
    background-color: pink;
}
 
 
html
  
<!-- HTML -->
<div class="box">
    <div class="item1">1</div>
    ...
    <div class="item9">9</div>
</div>
 
```
 
 
## 对齐方式
1. **justify-content**:  控制列轨道在容器内水平分布；
   **align-content**  控制行轨道在容器内垂直分布。
注：只有当容器尺寸大于所有轨道的总尺寸时，这两个属性才会生效。
2. **属性值**
  属性值 水平方向效果 垂直方向效果 

  start （默认值） 左对齐 顶部对齐 

 end  右对齐 底部对齐 

 center  水平居中对齐 垂直居中对齐 

 space-around  两侧留出相等空白，项目周围均匀分布 上下留出相等空白 

 space-between  首尾项目贴边 上下项目贴边 

 space-evenly  项目首尾与边空白相等 项目首尾与边空白相等 
 
 
 
## 做固定列的多行效果
```
css
  
/* CSS */
.content {
    /* 不要设置行轨道 */
    /* 给盒子高度 */
    display: grid;
    grid-template-columns: 160px 160px 160px 160px 160px;
    width: 1000px;
    margin: 0 auto;
    border: 1px solid red;
    justify-content: space-between;
}
.content div {
    height: 130px;
    background-color: pink;
    margin-bottom: 8px;
}
 
 
html
  
<!-- HTML -->
<div class="content">
    <div class="item1">1</div>
    ...
</div>
```
 
 
 
## gap  属性 &  repeat()  函数
 
1. fr ：分配轨道剩余空间的比例（ 1fr  表示一份，总为容器剩余空间， fr  是  fraction  缩写，意思是分数）
例： grid-template-columns: 1fr 2fr; （自动按比例分配布局，把网格分成两列，第一列占一份，第二列占两份）
2. 结合  fr  和  gap  属性的例子
```
css
  
.box {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows: 1fr 1fr 1fr;
    /* gap 可分开写：column-gap、row-gap，控制的是网格的间距，而非子元素 */
    gap: 10px;
    width: 300px;
    height: 300px;
    border: 1px solid red;
    margin: 20px;
}
.box div {
    background-color: pink;
}
 
 
html
  
<div class="box">
    <div class="item">1</div>
    ...
</div>
```
 
3. 结合  repeat()  函数的例子（多行或多列）
```
css
  
.nav {
    display: grid;
    grid-template-columns: repeat(11, 1fr);
    grid-template-rows: 1fr 1fr;
    gap: 10px;
    width: 935px;
    height: 66px;
    margin: 100px auto;
}
.nav a {
    background-color: #F6F7F8;
    border-radius: 6px;
    border: 1px solid #F1F2F3;
    /* 可补充的样式 */
    text-align: center;
    line-height: 28px;
    font-size: 14px;
}
 
 
html
  
<div class="nav">
    <a href=" ">1</a >
    ...
    <a href="#">11</a >
</div>
```
 
 
 
 **repeat()  函数**
 
- 语法： repeat(次数, 轨道尺寸)  或  repeat(自动填充, 轨道尺寸) 
- 固定次数： grid-template-columns: repeat(3, 1fr); 
 
 
 
## auto-fit  自动填充完成响应式效果
 
1. 效果实现要用到的函数：
-  repeat()  函数 +  auto-fit / auto-fill （自动填充，轨道尺寸）
-  auto-fill ：当容器空间大于所有轨道宽度时，会尽可能多地创建列，多余轨道保留空白
-  auto-fit ：当容器空间大于所有轨道宽度时，会合并空白并将空间分配给现有轨道，列宽会拉伸，响应式布局中更常用
-  minmax()  函数
- 语法： minmax(最小值, 最大值) 
- 作用：限制轨道的最小和最大宽度，保证列宽不会小于最小值
2. 例子
```
css
  
.box {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
    width: 80%;
    height: 300px;
    border: 1px solid red;
    margin: 50px auto;
}
.box .item {
    height: 120px;
    background-color: pink;
}
 
 
html
  
<div class="box">
    <div class="item">1</div>
    ...
</div>
```
 
 
 
## 网格线
 
1. 使用场景：实现元素跨越多格网格单元（线编号从1开始计算，3列就会有4根线）
2. 如何实现元素跨越多个网格单元？
- **语法1：**
- 跨列： grid-column: 开始线编号 / 结束线编号 
- 跨行： grid-row: 开始线编号 / 结束线编号 
例： grid-column: 1 / 3; （表示从第1列线到第3列线，跨2个单元格）
- **语法2：**
- 跨列： grid-column: 开始线编号 / span 单元格数量 
- 跨行： grid-row: 开始线编号 / span 单元格数量 
例： grid-column: 1 / span 2; （从1号线开始，跨2个单元格）
3. 例子
```
css
  
.box {
    border: 1px solid red;
    margin: 100px auto;
}
.box .item {
    height: 120px;
    background-color: pink;
}
/* CSS的伪类选择器：选中类名为box的元素中第一个类名为item的子元素 */
.box .item:first-child {
    grid-column: 1 / span 2;
    grid-row: 1 / span 2;
    height: auto;
}
 
 
html
  
<div class="box">
    <div class="item">1</div>
    ...
</div>
```
 
 
 
## 网格填充方式
 
 1. grid-auto-flow: row; （默认）：子元素按先行后列顺序填充，优先填满一行后换行
2. grid-auto-flow: column; ：子元素按先列后行顺序填充，优先填满一列后换列
3. 例子
```
css
  
.box {
    overflow: hidden; /* 使圆角有效果，切割掉多余部分 */
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: 1fr 1fr;
    grid-auto-flow: column;
    gap: 20px;
    max-width: 1760px;
    height: 900px;
    margin: 100px auto;
    border-radius: 20px;
}
.box img {
    display: block; /* 解决图片下方的空白缝隙 */
    width: 100%;
    height: 100%;
}
.box .item {
    background-color: pink;
}
.box .item:first-child {
    grid-row: 1 / 3;
}
.box .item:nth-child(3) {
    grid-column: 2 / 4;
    grid-row: 2 / 3;
}
 
 
html
  
<div class="box">
    <div class="item">
        < img src="...">
    </div>
    ...
    <div class="item">
        < img src="...">
    </div>
</div>
```
 
# 媒体查询
1. 定义：媒体查询能在不同的条件下使用不同的样式，是页面在不同的终端设备下达到不同的渲染效果。
2. 媒体查询的使用方法：
   @media 媒体类型and (媒体特性) {}
3. 媒体特性是通过min/max来表示大于等于或小于作为逻辑判断，而不是使用大于小于这种符号来判断
4. 判断方法：
 **最大宽度max-width**:媒体类型小于或等于指定的宽度时，样式生效
```
@media screen and (max-width:480px){
    .ads{
        display:none;
    }
}
这个表示的是当屏幕小于或等于480px时，页面中的ads区块将会被隐藏
```
**min-width**:指的是媒体类型大于胡等于指定宽度时，样式生效
```
@media screen and (min-width:900px){
    .wrapper{
        width:980px;
    }
}
这个表示媒体类型大于等于900px时，容器.wrapper的宽度变为980px
```
**多个媒体特性的使用**：媒体查询可以使用关键字and将多个媒体特性结合在一起
```
@media screen and (min-width:600px) and(max-width:900px){
    body{
        background-color:#f5f5f5
    }
}这个表示当在600px~900px之间时，body的背景颜色为#f5f5f5
```
**Device Width**:在智能设备上，例如iPhone，iPad等，还可以根据屏幕设备的尺寸来设置相应的样式（或者调用相应的样式文件）。同样的，对于屏幕设备同样可以使用min/max对应参数，如min-device-width或者max-device-width
```
<link rel="stylesheet" media="screen and (max-devixe-width:480px)" href="iphone.css"/>
这个的意思是iPhone.css样式适用的最大设备宽度是480px比如说iPhone上的显示，这里的“max-device-width”所指的是设备的实际分辨率，也就是可视面积分辨率
```
**not**:使用关键字not是用来排除符号表达式的设备，换句话说not关键词对后面的表达式执行取反操作
```
@media not print and (max-width:1200px){样式代码}
这个表示的是样式代码将被使用在除了打印设备和和设备宽度小于1200px下的所有设备中
```
**only关键词**用来指定某种特定的媒体类型，可以用来排除不支持媒体查询的浏览器




# object-fit  图片缩放
 
1. object-fit  是CSS中用于控制替换元素（如  `<img>` 、 `<video>` 、 `<iframe>`  等加载外部资源的元素）的属性：
-  fill （默认值）：拉伸内容以完全填充容器，不保持宽高比，可能导致内容变形（最常用）
-  contain ：保持内容固有宽高比，缩放至完全适配容器内，内容全可见，容器可能有空白
-  cover ：保持宽高比，缩放至覆盖容器（内容可能部分被裁剪），容器无空白
- 配合  object-position ：控制内容在容器内的对齐位置（如  center  居中、 left  左上角），常与  object-fit  搭配使用（例如  cover  时调整裁剪区域）
2. 例子（接上方例子）
```
在  .box img  样式中增补：
css
  
object-fit: cover;
object-position: center;
```

# CSS 书写顺序
 
合理的 CSS 属性书写顺序应遵循**布局 → 盒模型 → 视觉 → 交互 → 其他**的逻辑，核心目标是让代码更易读、易维护，团队协作中保持一致性是关键。
 
1. 布局相关属性：控制元素整体位置和层级，优先写在最前面。包括  display 、 visibility 、 position 、 top/right/bottom/left 、 float 、 clear 、 overflow 、 z-index 、 clip  等。
2. 盒模型相关属性：定义元素的尺寸、内外边距和边框，紧随布局之后。包括  box-sizing 、 width/min-width/max-width 、 height/min-height/max-height 、 margin 、 padding 、 border 、 outline  等。
3. 视觉样式属性：处理元素的颜色、背景、字体等外观表现。包括  color 、 background 、 font 、 font-family 、 font-size 、 line-height 、 text-align 、 text-indent 、 letter-spacing 、 white-space  等。
4. 交互与动画属性：控制元素的鼠标状态、过渡和动画效果。包括  cursor 、 opacity 、 transition 、 animation 、 transform  等。
5. 其他低频属性：特殊或较少使用的属性，放在最后。包括  filter 、 clip-path 、 backdrop-filter 、 will-change 、 touch-action 、 scroll-behavior  等。
 
 
 
# CSS 鼠标样式（cursor 属性）
 
在 CSS 中， cursor  属性用于控制鼠标指针在元素上的显示样式，通过改变光标形态可以向用户传递交互提示，提升界面体验。常见值及含义如下：
 
-  default ：默认箭头光标，通常是系统默认样式。
-  pointer ：手型光标，常用于可点击元素，如链接、按钮。
-  text ：I型竖线光标，用于文本输入区域，如文本框、可编辑内容。
-  wait ：等待状态光标，如旋转圆圈或沙漏，表示操作正在进行中。
-  help ：带问号的箭头光标，提示用户当前区域可获取帮助信息。
-  not-allowed ：禁止状态光标，如圆圈带斜线，表示操作不可用，比如禁用的按钮。
-  grab ：抓取状态手型，表示元素可被拖动。
-  grabbing ：抓取中状态手型，表示元素正在被拖动。
-  zoom-in ：放大状态光标，如加号，表示可放大操作。
-  zoom-out ：缩小状态光标，如减号，表示可缩小操作。