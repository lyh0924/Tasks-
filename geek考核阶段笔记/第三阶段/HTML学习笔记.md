- [HTML学习笔记](#html学习笔记)
  - [标签关系](#标签关系)
  - [标题和段落](#标题和段落)
  - [强调与重要标签](#强调与重要标签)
  - [图像标签以及常见格式](#图像标签以及常见格式)
  - [路径分类](#路径分类)
  - [音视频标签及下载方式](#音视频标签及下载方式)
  - [创建超链接以及锚点链接](#创建超链接以及锚点链接)
  - [网页结构标签和无语义标签](#网页结构标签和无语义标签)
  - [表格标签和合并单元格](#表格标签和合并单元格)
  - [表单容器，表单控件，辅助标签](#表单容器表单控件辅助标签)
# HTML学习笔记 
## 标签关系  
1. **并列关系**：`<head></head>`  `<body></body>`  
2. **嵌套关系**： 
```  
   <head>  
       <title></title>  
   </head>  
```  
## 标题和段落  
1. **标题标签**：  
   1.  从`<h1>`到`<h6>`一共有六级标题`<h1>html</h1>`就为一级标题
   2. h1具有唯一性  
   3. 标题的层级最好不要超过三层  
   4. 标题文字会加粗显示，并且每一行只显示一个     
2. **段落标签**：  
    1. `<p>和</p>`内写段落 
3. **语义化好处**：  
   * 更清晰的代码结构  
   * 对搜索引擎更友好  
   * 更好的可访问性  
## 强调与重要标签  
1. **强调标签** ： 
    1.  `<strong></strong>`：用来加粗文字 <strong>文字 </strong>
    2. `<em></em>`：使文字倾斜  <em>文字</em>
    3.  `<ins></ins>`:下划线  <ins>文字</ins>  
    4.  `<del></del>`：删除线  <del>文字</del>  
2. **注释标签**：不会在浏览器中显示
    1. `<!--这里写注释内容-->` 
       快捷键：ctrl+/  
    2. 可以跨越多行  
 3. **元素分类**  
    1. 块级元素  
    * 块级元素独占一行  
    * 可以嵌套其他元素  
    * 如：`<p><h><div>` （p标签内不要放其他块级元素） 
    1. 内联元素 （行内元素） 
    * 可以一行放多个，通常与文本一起使用  
    * 不能嵌套块级元素，可以嵌套其他内联元素  
    * 如：`<strong><em><a>` 等  
## 图像标签以及常见格式  
1. **图像标签**：   
    1. 注意：
      * 属性采取键值对形式，属性=值  
    * 属性之间没有必要的先后顺序  
   * 属性之间一定要有空格分隔
    1. 语法：`<img src="" alt="">`(属性之间要有空格)
    * src属性：要插入到页面的图像地址  
    * alt属性：备选文本，在网速较慢或者图片无法显示状况下的文字  
    1. 其他属性  
    * width：设置图片宽度 （宽度高度修改一个即可，另一个等比例缩放）
    * height：设置图片高度  
    * title：图像标题，鼠标悬停显示的文本 
2. **常见格式**  
    1. 网页优化：优先Webp/AVIF(兼容时)，备选JPEG/PNG  
    2. 透明图像：PNG（静态）或Webp(动态)  
    3. 动画：WebP/GIF（简单动画）  
## 路径分类  
1. **相对路径**   
    1. 同一级路径（./表示在当前文件夹）
    `<img src="pig.jpg" alt="这是小猪">`
    或`<img src="./pig.jpg" alt="这是小猪">`   
    2. 下一级路径(使用目录名/文件名)  
    `<img src="img/pig.jpg" alt="这是小猪">`
    3. 上一级路径（使用../返回上一级）  
    `<img src="../pig.jpg" alt="这是小猪">`  
2. **绝对路径**   
   从根目录开始的完整路径，包含完整的URL地址  
   * 从盘符开始：  
  `<img src="E:\HTML5\代码\pig.jpg" alt="tupian">` （不推荐） 
   * 完整地址： 
`<img src="https://www.example.com/images/pig.jpg" alt="tupian">`  
## 音视频标签及下载方式  
1. **语法**    
   `<video src=""></video>`  
   如：`<video src="video.mp4" controls=controls width="300"></video>`    
   **如果属性的键和值是相同的，则可以省略值**  
   把controls=controls 改为controls
2. **属性**：  
   * src:指向要插入到页面的视频地址  
   * controls：显示浏览器自带播放的控件  
   * width/height属性：设置视频的宽度与高度  
   * autoplay:自动播放 （要自动播放首先要静音） 
   * loop：循环播放  
   * muted：静音  
   * poster：预览图像（视频封面）  
3. **视频标签兼容性写法**：  
```  
<video controls>  
  <source src="video.mp4" type="video/mp4">
  <source src="video.ogg" type="video/ogg">
  <source src="video.webm" type="video/webm">
  <p>您的浏览器不支持HTML5Video标签，请升级浏览器。</p>
</video>
```  
* 将src属性放在几个单独的`<source>`元素当中，这些元素分别指向各自的资源  
* 浏览器会检查`<source>`元素，并播放第一个与其自身相匹配的媒体  
* 每个`<source>`元素中都含有type属性，浏览器会通过检查这属性来迅速跳过那些不支持的格式，能节省大量的时间和资源   
4. **视频标签兼容性写法**：  
   简单版：` <audio src="audio.mp3"></audio>` （音频标签浏览器不让自动播放）   
   兼容性：
   ```  
   <audio autoplay>
     <source src="audio.mp3" type="audio/mp3">  
     <p>您的浏览器不支持 HTML 5 Audio 标签，请升级浏览器。</p>  
   </audio>  
   ```  

## 创建超链接以及锚点链接    
1. **语法**
* `<a href=""></a>`
如:`<a href="https://www.deepseek.com/">Deepseek宫网</a>`
链接可包含除了自身以来的其它元素，比如**文字、标题、视频**等
2. **超链接种类**
    1. **内部链接**
如`<a href="./11-音频标签，html">音频</a>`
    1. **外部链接**
如`<a href="http://www.deepseek.com/">deepseek</a>`
3. **属性**  
    1. **href属性**(也称为超文本引用或目标，将包含一个网址)来创建一个基本链接
    2. **title**：鼠标悬停的提示文字
    3. **target**:
    * _self:当前窗口打开(默认)
    * _blank：新窗口打开
如：`<a href="https://www.depseek.com/" title="deepseek" target="_blank">deepseek</a>`
4. **链接**
    1. **空链接**
    通常指的是没有实际指向目标的超链接，符号是#
`<a href="#">产品介绍</a>`
    2. **下载链接**
   如果是exe或压缩包点击是下载
`<a href="./download.zip">下载软件</a>`
    3. **邮件链接**
  某些简单场景或个人使用情况下使用.
`<a href="mailto:123@qq.com>联系我</a>`
5. **锚点链接**
    1. 允许用户在同一页面内跳转到指定位置，适合长页面导航.
    2. 创建方法
        1. 定义锚点目标：使用id属性创建锚点目标，如：`<h2 id="1">第一部分</h2>`
        2. 创建跳转链接：使用#标记，如`<a href="#1">跳到第一部分</a>`
        3. `<br>`是换行标签，是单标签
        4. 跳转时多一个页面的滑动效果，在`<head></head>`标签中添加**下侧代码**  
```  
<style>
   html{
scroll-behavior:smooth;
   }
</style>  
```  
## 网页结构标签和无语义标签  
1. 网页的外观多种多样，但是大概都包含：页眉、导航栏、主内容、侧边栏、页脚等
`<header>`:网页页眉（头部）
`<main>`:网页内容 每个页面只能有一个
`<nav>`:导航栏
`<article>`:文章相关
`<section>`:分块
`<aside>`:侧边栏
`<footer>`:页面页脚(底部)
2. 无语义标签
    1. **div标签**
特点：
1.块级元素：默认独占一行，前后会自动换行
2.通常用于布局结构，作为其他元素的容器
3.可以包含其他块级或行内元素
4.默认没有语义
    2. **span标签**
特点：
1.行内元素：不会换行，仅包裹内容的一部分
2.用于对文本或行内元素的局部样式或操作
3.默认没有语义
3. **列表标签**
   1. **无序列表 ul**
   无序列表与顺序无关
```
<ul>
  <li>猪爸爸</li>
  <li>猪妈妈</li>
  <li>佩奇</li>
  <li>乔治</li>
</ul>
```    

   `<ul>`:
   * 定义列表的容器
   * 只能包含`<li>` 元素
  
   `<li>`:
   * 定义列表的选项
   * 里面可以放其他html元素

      2. **有序列表  ol** 
有序列表与顺序有关
```
<ol>
<li>看视频</li>
<li>写代码</li>
<li>做笔记</li>
<li>多复习</li>
<ol>
```
`<ol>`:
* 定义列表的容器
* 只能包含`<li>`元素   
  
`<li>`:
* 定义列表的选项
* 里面可以放其他html元素   
  
    3. **描述列表 dl**：  
   ```  
   <dl>  
     <dt>家电</dt>  
     <dd>电视</dd>
     <dd>冰箱</dd>
     <dd>空调</dd>
   </dl>  
   ```  
   `<dl>`:
* 定义列表的容器
* 只能包含`<dt><dd>`元素  
    
  `<dt>`:  
* 定义被描述的术语  
* 通常显示为左对齐和加粗  
* 一个`<dt>`可以对应多个`<dd>`  

   `<dd>`:
* 包含术语的定义或描述  
* 通常显示为缩进形式  
* 可以包含段落，图片，链接等其他HTML元素  
## 表格标签和合并单元格  
1. **表格基本组成**：  
   * `<table>`:表格容器标签   
   * `<tr>`:行标签
   * `<td>`:单元格标签  
   * `<th>`:表头单元格（通常只用在第一行或第一列，让表格里的文字加粗，水平和垂直居中）  
  <table>
  <tr>
  <th>姓名</th>
  <th>年龄</th>
  <th>成绩</th>
  </tr>
  <tr>
   <td>张三</td>
  <td>18</td>
  <td>89</td>
  </tr>
  <tr>
   <td>李四</td>
  <td>17</td>
  <td>100</td>
  </tr>
  </table>

```  
 <table>
   <tr>
      <th>姓名</th>
      <th>年龄</th>
      <th>成绩</th>
   </tr>
   <tr>
      <td>张三</td>
      <td>18</td>
      <td>89</td>
   </tr>
   <tr>
      <td>李四</td>
      <td>17</td>
      <td>100</td>
   </tr>
  </table>  
  ```  
2. **表格的结构标签**  （结构更清晰）
   `<thead>`:定义表格的头部区域
   `<tbody>`:定义表格的主体部分
   `<tfoot>`:定义表格的底部区域    
   <table>
    <thead>
     <tr>
      <th>姓名</th>
      <th>年龄</th>
      <th>成绩</th>
     </tr>
    </thead>
    <tbody>
     <tr>
      <td>张三</td>
      <td>18</td>
      <td>89</td>
     </tr>
    </tbody>
     <tr>
      <td>李四</td>
      <td>17</td>
      <td>100</td>
     </tr>
   </table>  

   ```
   <table>
    <thead>
     <tr>
      <th>姓名</th>
      <th>年龄</th>
      <th>成绩</th>
     </tr>
    </thead>
    <tbody>
     <tr>
      <td>张三</td>
      <td>18</td>
      <td>89</td>
     </tr>
    </tbody>
     <tr>
      <td>李四</td>
      <td>17</td>
      <td>100</td>
     </tr>
   </table>  
   ```
3. **合并单元格**
    1. **原理**：  
       1. 确定是跨行（rowspan）还是跨列合并（colspan）
       2. 找到目标单元格（**左上原则**），**写合并数量**  
       3. 删除多余单元格
       
    2. **原表格**：  
<table>
    <thead>
     <tr>
      <th>姓名</th>
      <th>年龄</th>
      <th>居住地</th>
     </tr>
    </thead>
    <tbody>
     <tr>
      <td>张三</td>
      <td>18</td>
      <td>北京</td>
     </tr>
    </tbody>
     <tr>
      <td>李四</td>
      <td>17</td>
      <td>广西</td>
     </tr>
     <tr>
      <td>王五</td>
      <td>18</td>
      <td>广西</td>
     </tr>  
     <tr>  
     <td>
     日期
     </td>
     <td></td>  
     <td></td>    
     </tr>
   </table>    

1. 如：（**跨行合并：上原则**）
   <table>
    <thead>
     <tr>
      <th>姓名</th>
      <th>年龄</th>
      <th>居住地</th>
     </tr>
    </thead>
    <tbody>
     <tr>
      <td>张三</td>
      <td>18</td>
      <td>北京</td>
     </tr>
    </tbody>
     <tr>
      <td>李四</td>
      <td>17</td>
      <td rowspan="2">广西</td>
     </tr>
     <tr>
      <td>王五</td>
      <td>18</td>
     </tr>  
     <tr>  
     <td>
     日期
     </td>
     <td></td>  
     <td></td>    
     </tr>
   </table>    

   ```  

   如：**跨行合并**
   <table>
    <thead>
     <tr>
      <th>姓名</th>
      <th>年龄</th>
      <th>居住地</th>
     </tr>
    </thead>
    <tbody>
     <tr>
      <td>张三</td>
      <td>18</td>
      <td>北京</td>
     </tr>
    </tbody>
     <tr>
      <td>李四</td>
      <td>17</td>
      ***  <td rowspan=“2”>广西</td>  ***
     </tr>
     <tr>
      <td>王五</td>
      <td>18</td>
      <td>广西</td>//删除该行
     </tr>
   </table>    
   ```  
2. 如：（**跨列合并：左原则**）

<table>
    <thead>
     <tr>
      <th>姓名</th>
      <th>年龄</th>
      <th>居住地</th>
     </tr>
    </thead>
    <tbody>
     <tr>
      <td>张三</td>
      <td>18</td>
      <td>北京</td>
     </tr>
    </tbody>
     <tr>
      <td>李四</td>
      <td>17</td>
      <td>广西</td>
     </tr>
     <tr>
      <td>王五</td>
      <td>18</td>
      <td>广西</td>
     </tr>  
     <tr>  
     <td>
     日期
     </td>
     <td colspan="2"></td>     
     </tr>
   </table>


```    
<table>
    <thead>
     <tr>
      <th>姓名</th>
      <th>年龄</th>
      <th>居住地</th>
     </tr>
    </thead>
    <tbody>
     <tr>
      <td>张三</td>
      <td>18</td>
      <td>北京</td>
     </tr>
    </tbody>
     <tr>
      <td>李四</td>
      <td>17</td>
      <td>广西</td>
     </tr>
     <tr>
      <td>王五</td>
      <td>18</td>
      <td>广西</td>
     </tr>  
     <tr>  
     <td>
     日期
     </td>
     ***  <td colspan="2"></td>  ***
     <td></td>//把这行删掉     
     </tr>
   </table>  
```  
## 表单容器，表单控件，辅助标签  
1. **表单**  
   1. 用途：收集用户输入数据，并且将数据提交到后端进行处理  
   2. 使用场景：用户登录/注册   搜索框 联系表单 问卷调查 订单支付 文件上传  
2. 表单由**三部分**组成：  
   **第一部分：表单容器**：  
        * 作用：定义表单的容器，包裹所有表单控件  
        * 语法： `<form action=""></form>` 
      action属性定义了在提交表单的时候，应该把所收集的数据送给谁（URL）处理  
   **第二部分：表单控件**
**input**  
         可以创建文本输入框，密码框，单选框，复选框等  
          * 语法：`<input type="text">`(type属性定义了输入框的类型)  
          * type:**text**(单行文本框)
          * type：**password**（密码框）
          * type:**radio**(单选框)
          * type:**checkbox**(复选框)
          * type:**file**
          * 其他属性：
         **placeholder**:提示信息
         **name**:元素的名称  
         **maxlength**:允许最大的字符数  、
         **accesskey**:使元素获得焦点的快捷键  
         **autocomplete**:用于控制表单的自动填充行为，帮助浏览器决定是否根据用户历史输入，自动填充字段值取值**on/off**  
         **name**:表单名称实现分组（使一组只能选一个选项）
         **value**：表单值  
         **checked**：是否默认选中
         **multiple**:允许选择多个文件
         **accept**：规定选择的文件类型，多个类型之间用**逗号**分割
    
**示例** 
  * 账号：<input type="text" placeholder="请输入账号" name="usename">  
  * 密码：<input type="password" placeholder="请输入密码" maxlength="6" name="pwd">  
  ``` 
   账号：<input type="text" placeholder="请输入账号" name="usename">  
   密码：<input type="password" placeholder="请输入密码" maxlength="6" name="pwd">
    
```      
**示例：**
* 性别：<input type="radio" name="gender" value="0" checked>女                 <input type="radio" name="gender" value="1">男
（单选按钮的name属性不仅要写而且还要**相同**）  
* 爱好：<input type="checkbox" name="hpbby" value="0" checked>足球  <input type="checkbox" name="hobby" value="1">篮球 <input type="checkbox" name="hobby" value="2">羽毛球  
* 头像：<input type="file" name="file" multiple=".exe,.jpg">
```  
 性别：<input type="radio" name="gender" value="0" checked>女                 
      <input type="radio" name="gender" value="1">男
 爱好：<input type="checkbox" name="hpbby" value="0" checked>足球  
      <input type="checkbox" name="hobby" value="1">篮球 
      <input type="checkbox" name="hobby" value="2">羽毛球
 头像：<input type="file" name="file" multiple=".exe,.jpg">  
```  

**textarea**
1. `<textarea>`是一个多行纯文本编辑控件，适用于允许用户输入大量自由格式文本的场景，例如评论或反馈表单  
2. **常见属性**：  
   **name**：表单名称  
   **placeholder**:提示信息  
   **rows**：文本行数，正整数，默认为2  
   **cols**：文本列数，正整数，默认为20    
```
3. 示例 
 留言: <textarea name="msg" cols="30" rows="10" placeholder="请输入留言"> 
   ```
**select**  
1. 表示一个提供选型菜单的控件  
2. `<select>`元素是容器,`<option>`是每一个选项标签，每个选项要跟一个值，要想默认选中一个选项，可以添加**selscted**属性  
3. <select name="" id="">
    <option value="北京">北京</option>
    <option value="上海">上海</option>
    <option value="广西" selected>广西</option>
   </select>  

   ```
   <select name="" id="">
    <option value="北京">北京</option>
    <option value="上海">上海</option>
    <option value="广西" selected>广西</option>
   </select>
   ```
**button**  
1. 定义为一个按钮，元素内部可以放置内容，比如文本或图像  
2. 语法：`<button>内容</button>`  
3. 属性：disabled属性可以禁用按钮，无法点击  
4. <button>登录</button>
   <button disabled>登录</button>  

```
   <button>登录</button>
   <button disabled>登录</button>
```  
**第三部分：辅助标签**  
1. 辅助标签label
`<label>`表示用户界面中某个元素的说明。提升可访问性(点击标签可聚集输入格)

    1. **使用方式**
**方式一：利用for和id相关联**

<label for="nan">男</label>`
<input type="radio" id="nan" name="sex">


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**方式二：直接包含**
```
<label>男
<input type"radio" name="sex">
</label>
```
2. 字符实体：
    1. 是一段以连字号(&)开头，以分号(；)结尾的文本(字符串)，常用于显示保留字符和不可见的字符(如不换行空格)
    2. `&(&amp;)`
    `<(&lt;)`
      `>(&gt;)`
`"(&quot;)`
` (&nbsp;)` 空格
`-(&ndash;)` 短破折号
`—(&mdash;)` 长破折号
学习来源:[黑马pink讲前端](https://space.bilibili.com/415434293/lists?sid=6252199&spm_id_from=333.788.0.0)











