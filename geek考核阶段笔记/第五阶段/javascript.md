# JavaScript笔记
## 基本输入输出语法
### 文档输出内容
1. 语法一：
   作用：向body内输出内容
   注意：如果输出的内容写的是标签，也会被解析成网页元素
   ```
   document.write('要出的内容')
   ```
2. 语法二：
    作用：页面弹出警告对话框
    ```
    alert('要出的内容')
    ```
3. 语法三：
   作用：控制台输出语法，程序员调试使用
   ```
   console.log('控制台打印')
   ```
### 输入语法
1. 语法：`prompt('请输入你的姓名')`
2. 作用：显示一个对话框，对话框中包含一条文字信息，用来提示用户输入文字
3. 注意：alert()和prompt()他们两个会跳过页面渲染先被执行
   
## 变量的声明
1. 声明的语法:`let 变量名`

## 函数
### 函数的基本使用
1. **声明：**
   ```
   function 函数名(){
    函数体
    }
   ```
2. **调用(可以被多次调用)**：`函数名()`
### 匿名函数
1. **定义:**  没有名字的函数无法被直接调用
2. **使用方式：（函数表达式）**
   1. **函数表达式**：将匿名函数赋值给一个变量，并且通过变量名称进行调用，称这个为函数表达式
   2. **调用方式：** 先声明再使用
   ```
   let fn=function (x,y){
      console.log(x+y)
   }声明
   fn(1,2)调用
   ```
3. **使用方式:（立即执行函数）**
   1.  **使用场景：** 避免全局变量之间的污染
   2.  **要求：** 立即执行函数写完必须要加分号
   3.  **语法一**
   ```
   (function(){
      函数具体实现内容
   })();
   具体例子：
   (function(x,y){
      console.log(x+y)
   })(1,2)
   ```
   4. **语法二**
   ```
   (function(){}())
   ```
   5. **例子**
   ```
   输入秒数，可以自动转化为时分秒
   let second=+prompt('请输入秒数：')
   function getTime(t){
   let h=parseInt(t/60%24)
   let m=parseInt(t/60%60)
   let s=parseInt(h,m,s)
   h=h<10?'0'+h:h
   m=m<10?'0'+m:m
   s=s<10?'0'+s:s
   return '转换完毕之后是${h}时${m}分${s}秒'}
   let str=getTime(second)
   document.write(str)
   !!! parseInt：把字符串转整数，从左往右读取数字，读到非数字就停止
   !!! ${变量名}：表示把变量里面的值替换到文字里（简化拼接）
   转换完毕之后是${h}时${m}分${s}秒等价于
   "转换完毕之后是"+h+"时"+m+"分"+s+"秒"
   !!! return后面如果是文字的话可以加双引号或者单引号，数字等不用加
   ```
### 函数的调用
1. **全局调用：**  直接用`函数名（）`
2. **构造函数调用：** 用new关键字调用函数，此时函数作为构造函数，用来创建对象实例
   1. **执行过程：** 
       1. 创建一个空对象{}
       2. 将构造函数的this绑定到这个空对象
       3. 执行构造函数代码，如果没有显示返回对象，则返回这个新对象
       4. 不用new调用时它就是普通函数，this会指向全局对象
```
function Person(name){
   this.name=name
}
const alice=new Person("Alice")
console.log(alice.name)//"Alice"
```
3. **函数方法调用：** 
   a. 当函数作为对象的方法被调用时，this指向调用它的对象
```
const obj={
   name:"Bob",
   sayName(){
      console.log(this.name)
   }
}
obj.sayName()
```

   b. 谁调用this就指向谁
   c. 方法被赋值给变量后，再调用会丢失this

```
const fn=obj.sayName;
fn()//全局调用，this指向undefined，输出undefined
``` 
1. **call方法调用：**
   1. **语法：** func.call(thisArg,arg1,arg2)
   2. **参数：** 第一个参数是this指向的对象，后面依次是函数的参数（逐个传递）
```
funtion greet(greeting){
   console.log(${greeting},I'm ${this.name})
}
const user={name:"Chalie"};
greet.call(user,"Hello")//"Hello,I'm Chalie"
```
1. **apply调用方法：**
   1. **语法：** func.apply(thisArg,[argArray])
   2. **参数：** 第一个参数是this指向的对象，第二个参数是参数数组/类数组
   3. **适用：** 参数数量不确定时，直接传数组更方便
```
function sum(a,b){
   return a+b
}
sum.apply(null,[1,2])//3
```
### 函数的作用域
1. **定义：** 作用域是在运行时代码中的某些特定部分中变量，函数和对象的可访问性，也就是作用域决定了代码区块中变量和其他资源的可见性
2. **全局作用域和函数作用域：** 
   1. **最外层函数和在最外层函数外面定义的变量拥有全局作用域**
   ```
   var outVariable = "我是最外层变量"; //最外层变量
    function outFun() { //最外层函数
    var inVariable = "内层变量";
    function innerFun() { //内层函数
        console.log(inVariable);
   }
    innerFun();
   }  
   console.log(outVariable); //我是最外层变量
   outFun(); //内层变量
   console.log(inVariable); //inVariable is not defined
   innerFun(); //innerFun is not defined
   ```
   2. **所有未定义直接赋值的变量自动声明为拥有全局作用域：**
   ```
   function outFun2() {
    variable = "未定义直接赋值的变量";
    var inVariable2 = "内层变量2";
   }
   outFun2();//要先执行这个函数，否则根本不知道里面是什么
   console.log(variable); //未定义直接赋值的变量
   console.log(inVariable2); //inVariable2 is not defined
   ```
   3. **作用域是分层的，内层作用域可以访问外层作用域的变量，反之则不行**
   ```
   function foo(a){
      var b=a*2
      function bar(c){
         console.log(a,b,c)
      }
      bar(b*3)
   }
   foo(2)//2,4,12
   第一个作用域是全局作用域，有标识符foo
   第二个作用域是作用域foo，有标识符a,bar,b
   第三个作用域是bar,仅有标识符c
   ```
   4. **块语句（大括号“｛｝”中间的语句），如 if 和 switch 条件语句或 for 和 while 循环语句，不像函数，它们不会创建一个新的作用域。在块语句中定义的变量将保留在它们已经存在的作用域中。**
   ```
   if (true) {
    // 'if' 条件语句块不会创建一个新的作用域
    var name = 'Hammad'; // name 依然在全局作用域中
   }
   console.log(name); // logs 'Hammad'
   ```
3. **块级作用域**
   1. 块级作用域可通过新增命令 let 和 const 声明，所声明的变量在指定块的作用域外无法被访问。块级作用域在如下情况被创建：
       1. 在一个函数内部
       2. 在一个代码块（由一对花括号包裹）内部
    2. let 声明的语法与 var 的语法一致。基本上可以用 let 来代替 var 进行变量声明，但会将变量的作用域限制在当前代码块中。若在一个块级作用域里面变量用var声明，则可在作用域外部访问，若用let声明则在作用域外访问会报错
    3. 块级作用域有以下几个特点：
       1. 声明变量不会提升到代码块顶部
       ```
       function getValue(condition) {
       if (condition) {
       let value = "blue";
       return value;
       } else {
       // value 在此处不可用
       return null;
       }
       // value 在此处不可用
       }
       ```

        2. 禁止重复声明
        ```
        如果一个标识符已经在代码块内部被定义，那么在此代码块内使用同一个标识符进行 let 声明就会导致抛出错误
        var count = 30;
        let count = 40; // Uncaught SyntaxError: Identifier 'count' has already been declared
        count 变量被声明了两次：一次使用 var ，另一次使用 let 。因为 let 不能在同一作用域内重复声明一个已有标识符，此处的 let 声明就会抛出错误。但如果在嵌套的作用域内使用 let 声明一个同名的新变量，则不会抛出错误。

        var count = 30;
        // 不会抛出错误
        if (condition) {
        let count = 40;
        // 其他代码
        }
        ``` 
### 作用域链
1. 自由变量：当前作用域没有定义的变量，这成为自由变量，自由变量的值应该向父级作用域寻找
```
var a = 100
function fn() {
    var b = 200
    console.log(a) // 这里的a在这里就是一个自由变量
    console.log(b)
}
fn()
```
2. 作用域链：如果没有父级的话，再一层一层向上寻找，直到找到全局作用域还是没找到，就宣布放弃，这种一层一层的关系，就是作用域链 
```
var a = 100
function F1() {
    var b = 200
    function F2() {
        var c = 300
        console.log(a) // 自由变量，顺作用域链向父作用域找
        console.log(b) // 自由变量，顺作用域链向父作用域找
        console.log(c) // 本作用域的变量
    }
    F2()
}
F1()
```  
3. 关于第一点的说法可能会产生歧义
```
var x = 10
function fn() {
  console.log(x)
}
function show(f) {
  var x = 20
  (function() {
    f() //10，而不是20
  })()
}
show(fn)

在 fn 函数中，取自由变量 x 的值时，要到创建 fn 函数的那个作用域中取，无论 fn 函数将在哪里调用,因此这个说法更为严谨

var a = 10
function fn() {
  var b = 20
  function bar() {
    console.log(a + b) //30
  }
  return bar
}
var x = fn(),
  b = 200
x() //bar()
fn()返回的是 bar 函数，赋值给 x。执行 x()，即执行 bar 函数代码。取 b 的值时，直接在 fn 作用域取出。取 a 的值时，试图在 fn 作用域取，但是取不到，只能转向创建 fn 的那个作用域中去查找，最后找到了,所以最后的结果是 30
```
### 垃圾回收机制
1. 内存中的生命周期
    1. 内存分配：当我们声明变量、函数、对象的时候，系统会自动为他们分配内存
    2. 内存使用：即读写内存，也就是使用变量、函数等
    3. 内存回收：使用完毕，由垃圾回收器自动回收不用的内存
2. 说明：全局变量一般不会被回收（关闭页面回收），一般情况下局部变量的值，不用了，会被自动回收掉
3. 内存泄漏：程序中分配的内存由于某种原因程序未释放或无法释放叫做内存泄漏
4. JS垃圾回收机制算法说明
    1. 栈（操作系统）：由操作系统自动分配释放函数的参数值、局部变量等，基本数据类型放到栈里面
    2. 堆（操作系统）：一般由程序员分配释放，若程序员不释放，由垃圾回收机制回收。复杂数据类型放到堆里面
5. 两种常见的垃圾回收算法
     1. **引用计数法**
     ```
     IE采用的引用计数算法，定义“内存不再使用”，就是看一个对象是否有指向他的引用，没有引用了就回收对象
     算法：
     1. 跟踪记录被引用的次数
     2. 如果被引用了一次，那么就记录次数1，多次引用会累加++
     3. 如果减少一个引用就减1—--
     4. 如果引用次数是0，则释放内存
     5. 存在一个致命性问题：嵌套引用（循环引用）
     如果两个对象相互引用，尽管他们已不再使用，垃圾回收器不会进行回收，导致内存泄漏
     如：
     function fn(){
        let o1={}
        let o2={}
        o1.a=o2
        o2.a=o1
        return '引用计数无法回收'
     }
     fn()
     因为他们的引用次数永远不会为0，这样的相互引用如果说很大量的存在就会导致大量的内存泄漏
     ``` 
     2. **标记清除法**
     ```
     现代浏览器通用的大多是基于标记清除法的某些改进算法，总体思想都是一样的
     核心：
     1. 标记清除算法将‘不再使用的对象’定义为“无法到达的对象”
     2. 就是从根部（在JS中就是全局对象）出发定时扫描内存中的对象。凡是能从根部到达的对象，都是还需要使用的
     3. 那些无法由根部出发触及到的对象被标记为不再使用，稍后进行回收，这就解决了引用计数法的弊端
     ```
   
### 闭包
1. 概念：一个函数对周围状态的引用捆绑在一起，内层函数中访问到其外层函数的作用域（简单理解：闭包=内层函数+外层函数的变量）
2. 作用：封闭数据，提供操作，外部也可以访问函数内部的变量
3. 简单的闭包代码
```
function outer(){
    const a=1
    function f(){
        console.log(a)
    }
    f()
}
outer()
```
4. 常见的的闭包形式(外部可以访问使用函数内部的变量)
```
function outer(){
    let a=100
    function fn(){
        console.log(a)
    }
    return fn
}
//outer() == fn == function fn() {}
//const fun = function fn() {}
const fun =outer()
fun()//调用函数
```
5. 例子：要做一个统计函数调用次数，函数调用次数，就++(闭包的应用)
```
function count(){
    let i=0
    function fn(){
        i++
        console.log('函数被调用了${i}次')
    }
    return fn
}
const fun=count()
在此闭包里面根据标记清除法可知，i能被找到，故i不会被回收，故会内存泄漏
所以闭包会产生内存泄漏的风险
```    
6. 两段代码比较体现闭包特性
```
第一段
function a(){
    var n = 0;
    function inc() {
        n++;
        console.log(n);
    }
    inc();  
    inc(); 
}
a(); //控制台输出1，再输出2

1. inc在a函数内部直接调用，执行完两次打印后，函数 a 运行结束；函数执行完毕，内部 n 、 inc 全部销毁，外部无法访问 inc ，出了a就不能再调用
2. 外部完全拿不到 inc ，只能在a内部调用
3. inc是普通内部函数，仅局部可见

第二段
function a(){
    var n = 0;
    this.inc = function () {
        n++; 
        console.log(n);
    };
}
var c = new a();
c.inc();    //控制台输出1
c.inc();    //控制台输出2
1. 用 new a() 创建实例 c ，把内层函数挂载到实例 this 上；a 函数执行完毕，但实例c持有inc函数，外部可以随时多次调用 c.inc() ；变量 n 被inc函数留住，不会被垃圾回收销毁
2. 外部变量 c 可以无限次调用 inc()
3. inc 成为实例对象 c 的方法

第二段代码如何体现闭包三大核心特点
 
特点1：内层函数可以读取外层函数局部变量 
inc 内部直接使用 var n = 0 ， n 是外层a的局部变量，正常函数外部无法访问，内层函数却能读取、修改
 
特点2：外层函数执行结束，局部变量不会销毁
执行 new a() 时，a函数从头到尾跑完，理论上局部变量 n 应该被回收
但因为 this.inc 函数引用了 n ，形成闭包， n 会一直保存在内存中
第一次 c.inc()  → n=1
第二次 c.inc()  → n=2
数值会保留上次修改后的状态，不会每次重置为0
 
特点3：让外部作用域间接操作私有变量 
变量 n 是私有变量，外部代码不能直接修改 c.n （访问不到），只能通过暴露的 inc() 方法去修改，实现数据私有化
```
### 定时器
**间歇函数**
1. 使用场景：网页中的倒计时等
2. 开启定时器：`setInterval(函数，间隔时间)`
   作用：每隔一段时间调用这个函数，间隔时间单位是毫秒
3. 关闭方法：`clearInterval()`  
3. 定时器返回的是一个数字
4. 每隔一秒种调用一次
```
<body>
  <script>
     //1. 匿名函数
     setInterval(function (){
        console.log('一秒被执行一次')
     }，1000)
     //2. 有函数名
     function fn(){
        console.log('一秒执行一次')
        //尽量用let，因为定时器时开时关
        let n=setInterval(fn,1000)//函数名不要加小括号
        clearInterval(n)
     } 
  </script>
</body>
```
**setTimeout**
`setTimeout(handle,1000)`两个参数：要执行的函数，设定时间（单位为ms）
`clearTimeout()`
### 正则表达式
1. **正则表达式的创建方式**  
    1. **字面量创建方式**   ` var reg = /pattern/flags`
    2. **实例创建方式**  `var reg = new RegExp(pattern,flags);`
    3. `pattern:正则表达式  flags:标识(修饰符)`
    4.  标识主要包括：
        1. **i** 忽略大小写匹配
        2. **m** 多行匹配，即在到达一行文本末尾时还会继续寻常下一行中是否与正则匹配的项
        3. **g** 全局匹配 模式应用于所有字符串，而非在找到第一个匹配项时停止
   1. **字面量创建方式和构造函数创建方式的区别**
```
字面量创建方式不能进行字符串拼接，实例创建方式可以
var regParam = 'cm';
var reg1 = new RegExp(regParam+'1');
var reg2 = /regParam/;
console.log(reg1);  //   /cm1/
console.log(reg2);  //  /regParam/
```
```
字面量创建方式特殊含义的字符不需要转义，实例创建方式需要转义
var reg1 = new RegExp('\d');  //    /d/ 
var reg2 = new RegExp('\\d')  //   /\d/
var reg3 = /\d/;              //  /\d/ 
```
1. **元字符**
```
代表特殊含义的元字符
\d : 0-9之间的任意一个数字  \d只占一个位置
\w : 数字，字母 ，下划线 0-9 a-z A-Z _
\s : 空格或者空白等
\D : 除了\d
\W : 除了\w
\S : 除了\s
 . : 除了\n之外的任意一个字符
 \ : 转义字符
 | : 或者
() : 分组
\n : 匹配换行符
\b : 匹配边界 字符串的开头和结尾 空格的两边都是边界 => 不占用字符串位数
 ^ : 限定开始位置 => 本身不占位置
 $ : 限定结束位置 => 本身不占位置
[a-z] : 任意字母 []中的表示任意一个都可以
[^a-z] : 非字母 []中^代表除了
[abc] : abc三个字母中的任何一个 [^abc]除了这三个字母中的任何一个字符

代表次数的量词元字符
* : 0到多个
+ : 1到多个
? : 0次或1次 可有可无
{n} : 正好n次；
{n,} : n到多次
{n,m} : n次到m次
```
3. **正则运算符的优先级**
正则表达式从左到右进行计算，并遵循优先级顺序，这与算术表达式非常类似
相同优先级的会从左到右进行运算，不同优先级的运算先高后低
```
下面是常见的运算符的优先级排列
依次从最高到最低说明各种正则表达式运算符的优先级顺序：

\ :	转义符
(), (?:), (?=), []	=> 圆括号和方括号
*, +, ?, {n}, {n,}, {n,m}   => 量词限定符
^, $, \任何元字符、任何字符 
|   	=> 替换，"或"操作
```
4. **正则的特性**
```
贪婪性
所谓的贪婪性就是正则在捕获时，每一次会尽可能多的去捕获符合条件的内容。
如果我们想尽可能的少的去捕获符合条件的字符串的话，可以在量词元字符后加?

懒惰性
懒惰性则是正则在成功捕获一次后不管后边的字符串有没有符合条件的都不再捕获。
如果想捕获目标中所有符合条件的字符串的话，我们可以用标识符g来标明是全局捕获

var str = '123aaa456';
var reg = /\d+/;  //只捕获一次,一次尽可能多的捕获
var res = str.match(reg)
console.log(res)
// ["123", index: 0, input: "123aaa456"]
reg = /\d+?/g; //解决贪婪性、懒惰性
res = str.match(reg)
console.log(res)
// ["1", "2", "3", "4", "5", "6"]
```
[js正则表达式的验证大全](https://www.cnblogs.com/chenmeng0818/p/6370819.html)

### 事件
####  DOM的介绍

1. **DOM定义**：全称为document object model（文档对象模型）
2. **文档：** 一个页面就是一个文档，DOM中使用document表示
3. **元素：** 页面中的所有标签都是元素，DOM中使用element表示
4. **节点：** 网页中的所有内容都是节点（标签，属性，文本，注释等），DOM中使用node表示
DOM把以上内容都看做是对象
#### 获取页面元素的方法
##### 根据ID获取
1. 使用getElementById()可以获取带有ID的元素对象，并且getElementById()返回一个匹配特定ID的元素
2. **语法**：var element=document.getElementById(id)
   
element是一个Element对象，如果当前文档中拥有特定ID的元素不存在则返回null；id是大小写敏感的字符串；返回值返回一个匹配到ID的DOM的Element对象，若在当前Document下没找到则返回null
```
<body>
    <div id="timer">2019-9-9</div>
    <script>
        var timer=document.getElementById('timer')
        console.log(timer)//<div id="timer">2019-9-9</div>
        console.log(typeof timer)//object
        console.dir(timer)//打印返回的元素对象，更好的查看里面的属性和方法
    </script>
</body>
```
##### 根据标签名获取
1. 使用getElementsTagName()方法可以返回带有指定标签名的对象的集合
2. 还可以获取某个元素（父元素）内部所有指定标签名的子元素
3. 语法：element.getElementByTagName('标签名')
4. 注意：父元素必须是单个对象（必须指明是哪一个元素对象），获取的时候不包括父元素自己
```
<body>
   <ul>
       <li>1</li>
       <li>2</li>
       <li>3</li>
       <li>4</li>
       <li>5</li>
   </ul>
   <ol id="ol">
       <li>生僻字</li>
       <li>生僻字</li>
       <li>生僻字</li>
       <li>生僻字</li>
   </ol>
   <script>
       var lis=doucument.getElementByTagName('li')
       console.log(lis)//返回的是获取过来元素对象的集合，以伪数组的形式存储的
       console.log(lis[0])//<li>1</li>
       //依次打印里面的元素对象可以采取遍历的方式
       for(var i=0;i<lis.length;i++){
         console.log(lis[i])
       }
       //如果页面只有一个li，返回的还是伪数组的形式
       //如果页面中没有这个元素返回的空的伪数组的形式

       //当有多个li标签的时候，可选中父元素从而获取他的子元素
       var ol=document.getElementById('ol')
       console.log(ol.getElementByTagName('li'))
   </script>
</body>
```
##### 通过HTML5新增的方法获取
1. **语法：** 
    1. document.getElementsByClassName('类名')//根据类名返回元素对象集合
    2. document.querySelector('选择器')//根据指定选择器返回第一个元素对象
    3. document.querySelectorAll('选择器')//根据指定选择器返回
```
<body>
    <div class="box">盒子1</div>
    <div class="box">盒子2</div>
    <div id="nav">
        <ul>
            <li>首页</li>
            <li>产品</li>
        </ul>
    </div>
    <script>
       //1. 根据类名获得某些元素集合
       var boxs=document.getElementsByClassName('box')
       console.log(boxs)//盒子1
                        //盒子2


       //2. querySelector返回指定选择器的第一个元素对象
       var firstBox=document.querySelector('.box')
       console.log(firstBox)//<div class="box">盒子1</div>

       var nav=document.querySelector('#nav')
       console.log(nav)//<div id="nav">···</div>

       var li=document.querySelector('li')
       console.log(li)//<li>首页</li>
       ！！！选择器需要加符号，类要加.，id要加#号


       //querySelectorAll()返回指定选择器的所有元素对象的集合
       var allBox=document.querySelectorAll(".box")
       console.log(allBox)//结果同1.
    </script>
</body>
```
##### 获取特殊元素
```
//1. 获取body元素
var bodyEle=document.body
console.log(bodyEle)
console.dir(bodyEle)

//2. 获取html元素
var htmlEle=document.documentElement
console.log(htmlEle)
```
#### 事件基础
1. **事件三要素：** 
```
<body>
    <button id="btn">唐伯虎</button>
    <script>
        //点击一个按钮，弹出对话框
        //1. 事件是有三部分组成的 事件源 事件类型 事件处理程序
        //(1) 事件源 事件被触发的按钮  谁   按钮
        var btn=document.getElementById('btn')
        //(2)事件类型  如何触发  什么事件  比如鼠标点击(onclick) 还是鼠标经过  还是键盘按下
        //(3)事件处理程序   通过一个函数赋值的方式  完成
        btn.onclick=function(){
            alert('点秋香')
        }
    </script>
</body>
```
2. **执行事件的步骤**
   1. 获取事件源
   2. 注册事件（绑定事件）
   3. 添加事件处理程序（采取函数赋值形式）
```
<body>
    <div>123</div>
    <script>
         //执行事件步骤
         //点击div  控制台输出  我被选中了
         //1. 获取事件源
         var div=document.querySelector('div')
         //2. 绑定事件 注册事件
         //div.onclick
         //3. 添加事件处理程序 
         div.onclick=function(){
             console.log('我被选中了')
         }
    </script>
</body>
```
3. **操作元素——修改元素内容**
```
<body>
    <button>显示当前系统时间</button>
    <div>某个时间</div>
    <script>
        //当我们点击了按钮，div里面的文字会发生变化
        //1. 获取元素
        var btn=document.querySelector('button')
        var div=document.querySelector('div')
        //2. 注册事件
        btn.onclick=function(){
            div.innerText='2026-7-7'
        }
    </script>
</body>
```
```
<body>
    <button>显示当前系统时间</button>
    <div>某个时间</div>
    <script>
        var btn=document.querySelector('button')
        var div=document.querySelector('div')
        btn.onclick=function(){
            div.innerText=getDate()
        }
        funtion getDate(){
           var date=new Date()
           var year=date.getFullYear();
           var month=date.getFullMonth()+1
           var dates=date.getDate()
           var arr=['星期日'，'星期一'，'星期二'，'星期三'，'星期四'，'星期五'，'星期六']
           var day=date.getDay()
           return '今天是：'+year+'年'+'month'+'月'+dates+'日'+arr[day] 
        }

        //元素可以不添加事件，自动显示
        var p=document.querySelector('p')
        p.innerText=getDate()
    </script>
</body>
```
```
element.innerText:从起始位置到终止位置的内容，但它去除html标签，同时空格和换行也会去掉
element.innerHTML：起始位置到终止位置的全部内容，包括HTML标签，同时保留空格和换行
这两个属性都是可读写的，可以获取元素里面的内容
```
4. **操作元素——修改元素属性**
```
<body>
    <button id="ldh">刘德华</button>
    <button id="zxy">张学友</button><br>
    <img src="images/ldh.jpg" alt="" title="刘德华">
    <script>
        //修改元素属性
        //1. 获取元素
        var ldh=document.getElementById('ldh')
        var zxy=document.getElementById('zxy')
        var img=document.querySelector('img')
        //2. 注册事件 处理程序
        zxy.onclick=function(){
            img.src='images/zxy.jpg'
            img.title='张学友'
        }
        ldh.onclick=function(){
            img.src='images/ldh.jpg'
            img.title='刘德华'
        }
    </script>
</body>
```
5. **操作元素——修改表单属性**
```
<body>
    <button>按钮</button>
    <input type="text" value="输入内容">
    <script>
        //1. 获取元素
        var btn=document.querySelector("button")
        var input=document.querySelector('input')
        //2. 注册事件 处理程序
        btn.onclick=function(){
            //表单里的值 文字内容是通过value来修改的
            input.value='被点击了'
            //如果想要某个表单被禁用 不能再点击disabled 要这个按钮button禁用
            btn.disabled=true//等同于this.disabled=true  this指向的是事件函数的调用者btn
        }
    </script>
</body>

```
6. **操作元素——样式属性**
```
可以通过js修改元素的大小，颜色，位置等样式
1. element.style 行内样式操作
2. element.className 类名样式操作
注意：js修改style样式操作，产生的是行内样式，css权重比较高
```
```
<style>
    div{
        width:200px;
        height:200px;
        background-color:pink;
    }
</style>
<body>
    <div></div>
    <script>
        //1. 获取元素
        var div=document.querySelector('div')
        //2. 注册事件 处理程序
        div.onclick=function(){
            //div.style里面的属性采取驼峰命名法
            this.style.backgroundColor='purple'
            this.style.width='250px'
        }
    </script>
</body>
```
7. 事件的三大核心概念
    1. **事件类型（type）**
发生了什么动作：click、input、scroll、keydown 等
    2. **事件目标（target）**
谁触发的事件：按钮、输入框、div、document 等
    1. **事件处理函数（handler）**
   动作发生后要执行的代码
8. **注册事件（绑定事件）：** 给元素添加事件，称为注册事件或者绑定事件，有两种注册方式
   1. **传统注册方式**
       1. 利用on开头的事件（如onclick）
       2. `<button onclick="alert('hi')"></button>`
       3. `btn.onclick=function(){}`
       4. 特点：注册事件的唯一性
       5. 同一个元素同一个事件只能设置一个处理函数将会覆盖前面注册的处理函数
9.  **方法监听注册方式**
    1. addEventListener()是一个方法
    2. IE9之前的IE不支持此方法，可使用attachEvent()代替
    3. 特点：同一个元素同一个事件可以注册多个监听器
    4. 按注册顺序依次执行
10. **例子**
```
<body>
    <button>传统注册事件</button>
    <button>方法监听注册事件</button>
    <script>
        var btns=document.querySelectorAll('button')
        //1. 传统方式注册事件
        btns[0].onclick=function(){
            alert('hi')
        }
        btns[0].onclick=function(){
            alert('how are you')
        }
        //2. 事件侦听注册事件 addEventListener
        //(1)里面的事件是字符串 必定加引号 而且不带on
        //(2)同一个元素 同一个事件可以添加多个侦听器（事件处理程序）
        btns[1].addEventListener('click',function(){
            alert(22)
        })
        btns[1].addEventListener('click',function(){
            alert(33)
        })
        //22和33会接连出现
    </script>
</body>
```
11. **attachEvent事件监听方式**（ie9之前的版本支持）
`evenTarget.attachEvent(eventNameWithOn,callback)`
evenTarget.attachEvent()方法将指定的监听器注册到evenTarget(目标对象)上，当该对象触发指定的事件时，指定的回调函数就会被执行
`evenNameWithOn`:事件类型字符串，比如onclick,onmouseover,这里要带on
`callback`:事件处理函数，当目标触发事件时回调函数被调用
```
<body>
    <button>ie9 attachEvent</button>
    <script>
        btns[2].attachEvent('onclick',function(){
        alert(11)
    })
    </script>
</body>
```
12. **删除事件(解绑事件)**
    1. 删除事件的方式
        1. 传统注册方式`eventTarget.onclick=null`
        2. 方法监听注册事件
        `evenTarget.removeEvenListener(type,listener[,usecapture])`   
        `evenTarget.detachEvent(eventNameWithOn,callback)`
```
<body>
    <div>1</div>
    <div>2</div>
    <div>3</div>
    <script>
        var divs=document.querySelectorAll('div')
        div[0].onclick=function(){
            alert(11)
            //1. 传统方式删除事件
            div[0].onclick=null
        }
        //2. removeEventListener  删除事件
        div[1].addEventListener('click',fn)

        function fn(){
            alert(22)
            divs[1].removeEventListener('click',fn)
        }
        //3.
        divs[2].attachEvent('onclick',fn1)
        function fn1(){
            alert(33)
            dics[2].detachEvent('onclick',fn1)
        }
    </script>
</body>
```
13. **addEventListener语法**
```
element.addEventListener(type，handler，false/true)
type:事件类型
handler:事件执行触发的函数
false/true:false为冒泡/true为捕获，参数是true，表示在捕获阶段调用事件处理程序；如果是false，表示在冒泡阶段调用事件处理程序。

事件捕获：父级元素先触发，子集元素后触发；
事件冒泡：子集元素先触发，父级元素后触发；

一般的绑定事件，都是采用冒泡方式，也就是使用false
```
14. **removeEventListener语法**
```
element.removeEventListener(type，handler，false/true)
```
 **例子**
```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
</head>
<body>
<input type="button" value="test1" id="btn1">
<input type="button" value="test2" id="btn2">
//定义两个按钮，一个 id 叫 btn1，一个 id 叫 btn2
<script>
    var btn1=document.getElementById("btn1");/*实名函数*/
    拿到 id 为 btn1 的按钮，存到变量 btn1 里
    var count=0;
    var handle1=function() {
        alert(count++);
        if (count == 3) {
            alert("事件结束")
            btn1.removeEventListener("click",handle1,false);
        }
    }
    btn1.addEventListener('click',handle1,false);


    var btn2=document.getElementById("btn2");/*匿名函数*/
    btn2.addEventListener("click",function(){
        alert(123);
        removeEventListener("click",function(){
            alert(123)
        },false)
    },false)
</script>
</body>
</html>

通过匿名函数是无法消除监听事件，只有通过实名函数才能。
```
#### DOM事件流
1. 事件流描述的是从页面中接受事件的顺序
2. 事件发生时会在元素节点之间按照特定的顺序传播，这个传播过程即DOM事件流
3. DOM事件流分为3个阶段：捕获阶段 当前目标阶段 冒泡阶段
```
    捕获阶段：Document->Element html->Element body->Element div
    冒泡阶段：Element div->Element body->Element html->Document
```
4. 注意：
   1. JS代码中只能执行捕获或者冒泡其中的一个阶段
   2. onclick和attachEvent只能得到冒泡阶段
   3. `addEventListener(type,listener[,useCapture])`第三个参数如果是true，表示在事件捕获阶段调用事件处理程序；如果是false（不写的话默认是false），表示在事件冒泡阶段调用事件处理程序
   4. 有些事件没有冒泡，比如onblur,onfocus,onmouseenter,onmouseleave
```
<body>
    <div class="father">
        <div class="son">son盒子</div>
    </div>
    <script>
        //1.捕获阶段:如果addEventListener第三个参数是true那么则处于捕获阶段document->html->body->father->son
        var son=document.querySelector('.son')
        son.addEventListener('click',function(){
            alert('son')
        },true)
        var father=document.querySelector('.father')
        father.addEventListener('click',funtion(){
            alert('father')
        },true)
        //先输出father再输出son

        //2. 冒泡阶段：如果addEventListener第三个参数是false或者省略那么则处于冒泡阶段son->father->body->html->document
        var son=document.querySelector('.son')
        son.addEventListener('click',function(){
            alert('son')
        },false)
        var father=document.querySelector('.father')
        father.addEventListener('click',funtion(){
            alert('father')
        },false)
        //先输出son再输出father
    </script>
</body>
```
#### 事件对象
1. **什么是事件对象**
```
<body>
    <div>123</div>
    <script>
        var div=document.querySelector('div')
        div.onclick=function(event){
            console.log(event)
        }
        div.addEventListener('click',function(event){
            console.log(event)
        })
        //1. event就是一个事件对象，写到侦听函数小括号里面，当作形参来看
        //2. 事件对象只有有了事件才会存在，是系统自动创建的，不需要传递参数
        //3. 事件对象是我们事件的一系列相关数据的集合跟事件相关的，比如鼠标点击里面就包含了鼠标的相关信息（鼠标坐标等），如果是键盘事件里面的就包含的键盘事件的信息，比如判断用户按下了哪个键
        //4. 事件对象的名字可以自己命名
        //5. 若事件对象有兼容性问题，可通过window.event
    </script>
</body>
```
2. **事件对象的常见属性和方法**
    1. e.target:返回触发事件的对象   （标准）
    2. e.srcElement:返回触发事件的对象（非标准）
    3. e.type:返回事件的类型，比如click mouseover不带on
    4. e.cancelBubble:该属性阻止冒泡（非标准）
    5. e.returnValue:该属性阻止默认事件（默认行为）（非标准）
    6. e.preventDefault():该方法阻止默认事件（默认行为）（标准）（比如不让链接跳转）
    7. e.stopPropagation():阻止冒泡（标准） 
3. **例子**
```
<body>
    <div>123</div>
    <ul>
       <li>abc</li>
       <li>abc</li>
       <li>abc</li>
    </ul>
    <script>
        //1. e.target返回的是触发事件的对象   this返回的是绑定事件的对象
        var div=document.querySelector('div')
        div.addEventListener('click',function(e){
            console.log(e.target)
            console.log(this)
        })
        var ul=document.querySelector('ul')
        ul.addEventListener('click',function(e){
            //给ul绑定了事件，那么this就指向ul
            console.log(this)
            //e.target指向我们点击的那个对象  谁触发了这个事件  我们点击的是li e.target指向的就是li
            console.log(e.target)
        })

        //兼容性
        div.onclick=function(e){
            e=e||window.event
            var target=e.target||e.srcElement
            console.log(target)
        }

        currentTarget是跟this很相似的属性
    </script>   
</body>
```
#### 阻止默认行为
```
<body>
    <div>123</div>
    <a href="https://www.baidu.com">百度</a>
    <form action="https://www.baidu.com">
        <input type="submit" value="提交" name="sub">
    </form>
    <script>
        //常见事件对象的属性和方法
        //1. 返回事件类型
        var div=document.querySelector('div')
        div.addEventListener('click',fn)
        div.addEventListener('mouseover',fn)
        div.addEventListener('mouseout',fn)
        function fn(e){
            console.log(e.type)
        }   
        //2. 阻止默认行为
        var a=document.querySelector('a')
        a.addEventListener('click',function(e){
            e.preventDefault()  //dom标准写法
        })
        //3. 传统的注册方式
        a.onclick=function(){
            //普通浏览器 e.preventDefault() 方法
            e.preventDefault()
            //低版本浏览器returnValue属性
            e.returnValue
            //也可以利用return false 也能阻止默认行为，没有兼容性问题  特点：return后面的代码无法执行，而且只局限于传统的注册方式
            return false
            alert(11)//无法执行
        }
    </script>
</body>
```
#### 阻止事件冒泡
```
<body>
    <div class="father">
        <div class="son">son盒子</div>
    </div>
    <script>
        
        var son=document.querySelector('.son')
        son.addEventListener('click',function(e){
            alert('son')
            e.stopPropagation()//标准
            e.cancelBubble=true//非标准
        },false)
        var father=document.querySelector('.father')
        father.addEventListener('click',funtion(e){
            alert('father')
            e.stopPropagation()
        },false)
        //先输出son再输出father
    </script>
</body>
```
#### 事件委托
1. **事件委托：** 事件委托也称为事件代理，在jQuery里面称为时间委派
2. **事件委托的原理：** 不是每个子节点单独设置事件监听器，而是将事件监听器设置在父节点上，然后利用冒泡原理影响设置每个子节点
3. **事件委托的作用：** 只操作了一次DOM，提高了程序的性能 
```
<body>
    <ul>
        <li>你好</li>
        <li>你好</li>
        <li>你好</li>
        <li>你好</li>
        <li>你好</li>
    </ul>
    <script>
        //事件委托的核心原理：给父节点添加侦听器，利用事件冒泡影响每一个子节点
        var ul=document.querySelector('ul')
        ul.addEventListener('click',function(e){
            alert('你好')
            e.target.style.backgroundColor='pink'
        })
    </script>
</body>
```
## 性能优化
### 防抖
1. 概念：单位时间内，频繁触发事件，只执行最后一次
2. 使用场景：
    1. 搜索框搜索输入。只需要用户最后一次输入完，再发送请求
    2. 手机号，邮箱验证输入检测
3. 要求：鼠标在盒子上移动，里面的数字就会变化+1
```
css
.box{
    width:500px;
    height:500px;
    background-color:#ccc
    color:#ffff
    text-align:center
    font-size:100px;
}
html
<div class="box"></div>
JS
const box=document.querySelector('.box')
let i=i
function  mouseMove(){
    box.innerHTML=i++
    //如果里面存在大量消耗性能的代码，比如dom操作，比如数据处理，可能造成卡顿
}
//添加事件
box.addEventListener('mousemove',mouseMove)
``` 
```
利用防抖来处理-鼠标滑过盒子显示文字（鼠标停止500ms之后，里面的数字才会变化+1）
实现方式：
1. lodash提供的防抖来处理
2. 手写一个防抖函数来处理
```
```
1.lodash:
 _.debounce(func,[wait=0],[options=])
  创建一个debounced（防抖动）函数,该函数会从上一次被调用后，延迟wait毫秒后调用func方法
<body>
  <div class="box"></div>
  <script src=".js/lodash.min.js"></script>
  <script>
     const box=document.querySelector('.box')
     let i=1
     function mouseMove(){
        box.innerHTML=i++
     }
     box.addEventListener('mousemove',_.debounce(mouseMove,500))
  </script>
</body>
```
```
2. 手写防抖函数
核心思路：
a. 声明一个定时器变量
b. 当鼠标每次滑动（事件触发）都判断是否有定时器了，如果有定时器先清除以前的定时器
c. 如果没有定时器先开启定时器，要记得存到变量里面去
d. 在定时器里面调用要执行的函数
<body>
  <script>
function debounce(fn,t){
    let timer
    //return 一个匿名函数
    return function(){
        if(timer) clearTimeout(timer)
        timer=setTimeout(function(){
            fn()
        },t)
    }
}
function mouseMove(){
        box.innerHTML=i++
     }
box.addEventListener('mousemove',debounce(mouseMove,500))
  </script>
</body>
```
### 节流
1. 节流：单位时间内，频繁触发事件，只执行一次
2. 使用场景：鼠标移动mousemove、页面尺寸缩放resize、滚动条滚动scroll
3. 要求：鼠标在盒子上移动，不管移动多少次，每隔500ms才+1
4. 实现方式：
    1. lodash提供的节流函数来处理
    2. 手写一个节流函数来处理
```
1.lodash:._throttle(func,[wait=0],[options=])创建一个节流函数，在wait秒内最多执行func一次的函数
<script>
  const box=document.querySelector('.box')
  let i=1
  function mouseMove(){
    box.innerHTML=i++
  }
  box.addEventListener('mousemove',_.throttle(mouseMove,3000))
</script>
```
```
2. 手写节流函数
核心思路：
节流的核心就是利用定时器（setTimeout）来实现
a. 声明一个定时器变量
b. 当鼠标每次滑动都先判断是否有定时器了，如果有定时器则不开启新定时器
c. 如果没有定时器则开启定时器，记得存到变量里面
 -定时器里面调用执行的函数
 -定时器里面要把定时器清空
function throttle(fn,t){
    let timer=null
    return function(){
        if(!timer){
            timer=setTimer(function(){
                fn()
                //清除定时器
                timer=null
                //在setTimeout中是无法删除定时器的，因为定时器还在运作，所以使用timer=null而不是clearTimeout(timer)
            },t)
        }
    }
}
const box=document.querySelector('.box')
  let i=1
  function mouseMove(){
    box.innerHTML=i++
  }
box.addEventListener('mousemove',throttle(mouseMove,3000))
```
## 严格模式
1. 严格模式在IE10以上版本的浏览器才会被支持，旧版本浏览器中会被忽略
2. 严格模式对正常的JS语义做了一些更改：
   1. 消除了JS语法的一些不合理，不严谨之处，减少了一些怪异行为
   2. 消除代码运行的不安全之处，保证代码运行的安全
   3. 提高编译器效率，增加运行速度
   4. 禁用了在ECMAscript的未来版本中可能会定义的一些语法，为未来新版本的JS做好铺垫，比如保留一些字，如：class,enum,export,extends,import,super不能做变量名
3. 开启严格模式：严格模式可以应用到整个脚本或个别函数中。因此在使用时，我们可以将严格模式分为为脚本开启严格模式和为函数开启严格模式两种情况
   1. 为整个脚本文件开启严格模式，需要在所有语句之前放一个特定语句"use strict"(或'use strict')
   ```
   <body>
       <script>
            'use strict'
             //下面的JS代码就会按照严格模式执行代码
       </script>
       //为了防止变量污染，或开启一个独立的作用域空间,用立即执行函数
       <script>
            (function(){
               'use strict'
                //下面的JS代码就会按照严格模式执行代码
            })()
       </script>
   </body>
   ```
   2. 为某个函数开启严格模式
   ```
   //此时只有fn函数开启了严格模式
   <body>
       <script>
            function fn(){
                'use strict'
            }
            function fun(){
                //里面的还是按照普通模式执行
            }
       </script>
   </body>
   ```
4. 严格模式中的变化
   1. 变量规定
   ```
   1. 在正常模式下，如果一个变量没有声明就赋值，默认是全局变量。严格模式禁用这种用法，变量都必须用var命令声明，然后再使用
   2. 严禁删除已经声明的变量，例如，delete x的语法就是错误的
   ```
   2. 严格模式下this指向问题
   ```
   1. 以前在全局作用域函数中的this指向window对象
   2. 严格模式下全局作用域中函数中的this是undefined
   function fn(){
    console.log(this)//undefined
   }
   fn()

   3. 以前构造函数时不加new也可以调用，当普通函数，this指向全局对象
   function star(){
    this.sex='男'
   }
   star()
   console.log(window.sex)//男

   4. 严格模式下，如果构造函数不加new调用，this会报错
   'use strict' 
   function star(){
    this.sex='男'
   }
   star()
   console.log(window.sex)//错误

   5. new实例化的构造函数指向创建的对象实例
   'use strict' 
   function star(){
    this.sex='男'
   }
   var ldh=new star()
   console.log(ldh.sex)//男

   6. 定时器this还是指向window
   'use strict' 
   setTimeout(function(){
    console.log(this)//依然指向window
   },2000)

   7. 事件、对象还是指向调用者
   ```
   3. 函数变化
   ```
   1. 函数不能有重名的参数
   2. 函数必须声明在顶层。新版本的JS会引入块级作用域，为了与新版本接轨，不允许在非函数的代码块内声明函数
   "use strict"
   if(true){
    function f(){}//语法错误
    f()
   }
   for(var i=0;i<5;i++){
    function f2(){}//语法错误
    f2()
   }
   function baz(){//合法
    function eit(){}//同样合法
   }
   ```

# JSON
1. 定义：是一种轻量级的数据交换格式，目前使用比较广泛
2. 在JS语言中，一切都是对象。因此，任何JS支持的类型都可以通过JSON来表示，例如字符串，数字，对象，数组等
```
语法格式和要求：
1. 对象表示为键值对
2. 数据由逗号分隔
3. 花括号保存对象
4. 方括号保存数组
```
3. JSON键值对是用来保存JS对象的一种方式，和JS对象的写法也大同小异，键/值对组合中的键名写在前面并用双引号包裹，使用冒号分隔，然后紧接值
```
{"name":"qingjiang"}
{"age":"3"}
{"sex":"男"}
```
4. JSON是JS对象的字符串表示法，它使用文本表示一个JS对象的信息，本质是一个字符串
```
var obj={a:'Hello',b:'World'}//这是一个对象
var json='{"a":"Hello","b":"World"}'//这是一个JSON字符串，本质是一个字符串
```
5. JSON和JS对象互转
   1. 要实现JSON字符串转换为JS对象，使用JSON.parse()方法
   var obj=JSON.parse('{"a":"Hello","b":"World"}')//结果是{a:'Hello',b:'World'}
   2. 要实现从JS对象转换为JSON字符串，使用JSON.stringfy()方法
   var json=JSON.stringfy({a:'Hello',b:'World'})//结果是'{"a":"Hello","b":"World"}'
6. JSON对象可以作为键名的一个值存在
```
"key3":{
    "name":"温泉",
    "QQ":"2715863"
}
//取值：key3.name等
```
7. JSON对象可以采用数组形式
```
1. "key4":[1,2,3,4]
2. "key5":["a","b","c"]
3. "key6":[{
    "name":"a",//key6[0].name
    "age":"17"//key6[0].name+key6[2].age=a 19
},
{
    "name":"b",
    "age":"18"
},
{
    "name":"c",
    "age":"19"
}]
4. "key7":null
```
# AJAX
## XML
 **定义：** XML是可扩展标记语言，被设计用来传输和存储数据，XML与HTML类似，不同的是HTML中都是预定义标签，而XML中没有预定义标签，全都是自定义标签，用来表示一些数据

## HTTP
1. HTTP协议【超文本传输协议】，协议详细规定了浏览器和万维网服务器之间互相通信的规则
2. 浏览器给服务器发的内容 叫做请求，而服务器给浏览器（客户端）返回的结果叫做响应


## 一、Ajax 核心概述
### 1\.1 什么是 Ajax？

**Ajax（Asynchronous JavaScript And XML）**：异步 JavaScript 和 XML，是一种**无需刷新整个页面**，即可与服务器进行数据交互、局部更新页面的前端技术方案。

本质：通过浏览器内置的 `XMLHttpRequest` /`Fetch` 对象，在后台发送 HTTP 请求、接收服务器响应，结合 JS 实现页面局部刷新。

### 1\.2 Ajax 核心特点

- **异步通信（核心通俗理解）**：请求发送后，JS 代码不会阻塞等待服务器结果，继续执行后续逻辑，等后台数据返回后，再自动触发回调处理结果，全程页面不卡顿、不用刷新

- **局部刷新**：只更新页面局部内容，无需重载整个页面，用户体验极佳

- **前后端分离基础**：前端专注页面展示，后端专注数据处理，通过接口传输数据

- **数据格式灵活**：早期使用 XML，现在主流使用 **JSON** 格式
1. 优点
    1. 可以不需要刷新页面与服务器端进行通信
    2. 允许根据用户事件来更新部分页面内容
1. 缺点
   1. 没有浏览历史，不能回退
   2. 存在跨域问题（同源）
   3. SEO不友好

### 1\.3 同步 vs 异步

- **同步请求**：发送请求后，页面卡死，等待服务器响应完成后，才能执行后续代码

- **异步请求**：发送请求后，代码继续执行，响应结果通过回调函数处理，页面无阻塞

### 1\.4 Ajax 应用场景

- 表单实时校验（用户名、手机号是否已注册）

- 列表无刷新分页、筛选、搜索

- 动态加载页面数据（下拉加载更多、懒加载）

- 聊天室实时消息、点赞、评论无刷新更新

- 上传文件进度监听、接口动态获取数据

## 二、Ajax 工作原理

### 2\.1 完整执行流程

1. 浏览器创建 `XMLHttpRequest` 异步请求对象

2. 配置请求方式、请求地址、同步/异步模式

3. 绑定监听函数，监听请求状态变化

4. 发送 HTTP 请求到后端服务器

5. 服务器接收请求，处理业务逻辑，返回数据（JSON/文本）

6. 浏览器监听状态变化，接收响应数据，通过 JS 局部更新页面

### 2\.2 核心对象：XMLHttpRequest

所有传统 Ajax 请求的核心，浏览器内置对象，无需手动引入，直接使用。

现代浏览器也支持 `Fetch API`（Promise 风格）。

## 三、原生 Ajax 完整语法

### 3\.1 基础四步写法

原生 Ajax 固定四步：**创建对象 =\> 初始化请求 =\> 监听状态 =\> 发送请求**

```javascript
// 1. 创建XMLHttpRequest对象
const xhr = new XMLHttpRequest();

// 2. 初始化请求：open(请求方式, 请求地址, 是否异步)
// 第三个参数：true=异步，false=同步（最好使用异步）
xhr.open('GET', 'http://localhost:3000/api/data', true);

// 3. 监听请求状态变化
xhr.onreadystatechange = function() {
  // readyState=4：请求完成，响应就绪
  // status=200：HTTP请求成功
  if (xhr.readyState === 4 && xhr.status === 200) {
  // === 严格相等：值一样 并且 类型也一样，才为 true
  // 获取服务器响应数据
    console.log(xhr.responseText);
  }
};

// 4. 发送请求
xhr.send(null); // GET请求send传null或不传

```

### 3\.2 核心属性详解

#### 3\.2\.1 readyState 请求状态码

表示 Ajax 请求的执行阶段，共 5 个状态：

- **0**：未初始化，未调用 open\(\)

- **1**：请求已建立，已调用 open\(\)，未发送请求

- **2**：请求已发送，响应头已接收

- **3**：正在接收响应数据（部分数据返回）

- **4**：**请求全部完成**，数据接收完毕（唯一可用状态）

#### 3\.2\.2 status HTTP 状态码

- **200**：请求成功

- **404**：请求地址不存在

- **403**：权限不足

- **500**：服务器内部错误

- **405**：请求方式不允许

#### 3\.2\.3 响应数据属性

- `xhr.responseText`：获取文本格式的响应数据（字符串）

- `xhr.responseXML`：获取 XML 格式响应数据（基本淘汰）

- `xhr.response`：通用响应数据（根据返回格式自动适配）

### 3\.3 GET 请求

特点：参数拼接在 URL 后面、参数公开、长度有限、无请求体、缓存可控

```javascript
// GET请求携带参数
const xhr = new XMLHttpRequest();
// 参数直接拼接在地址后  ?key1=value1&key2=value2
xhr.open('GET', 'http://localhost:3000/api/user?name=张三&age=20', true);

xhr.onreadystatechange = function() {
  if (xhr.readyState === 4 && xhr.status === 200) {
    // 解析JSON字符串为JS对象
    const res = JSON.parse(xhr.responseText);
    console.log('请求结果：', res);
  }
};

// GET请求send无需传参
xhr.send();

```

### 3\.4 POST 请求

特点：参数放在请求体、隐私性更好、无长度限制、适合提交表单/大量数据

```javascript
const xhr = new XMLHttpRequest();
xhr.open('POST', 'http://localhost:3000/api/login', true);

// POST请求必须设置请求头，告诉服务器请求体格式
xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');

xhr.onreadystatechange = function() {
  if (xhr.readyState === 4 && xhr.status === 200) {
    const res = JSON.parse(xhr.responseText);
    console.log('登录结果：', res);
  }
};

// POST参数通过send传递，格式：key=value&key2=value2
xhr.send('username=admin&password=123456');

```

### 3\.5 POST 传递 JSON 格式数据

前后端分离项目主流传参格式，必须修改请求头 \+ JSON 序列化参数

```javascript
const xhr = new XMLHttpRequest();
xhr.open('POST', 'http://localhost:3000/api/register', true);

// 设置JSON格式请求头
xhr.setRequestHeader('Content-Type', 'application/json;charset=utf-8');

xhr.onreadystatechange = function() {
  if (xhr.readyState === 4 && xhr.status === 200) {
    console.log(JSON.parse(xhr.responseText));
  }
};

// JS对象转JSON字符串
const data = { username: '李四', phone: '13800138000' };
xhr.send(JSON.stringify(data));

```

## 四、Ajax 错误处理与状态监听

### 4\.1 完整容错写法

处理请求失败、服务器报错、网络异常、请求超时等场景

```javascript
const xhr = new XMLHttpRequest();
xhr.open('GET', 'http://localhost:3000/api/data', true);

// 设置超时时间（毫秒）
xhr.timeout = 5000;
// 超时监听
xhr.ontimeout = function() {
  alert('请求超时，请重试！');
};

// 网络错误监听
xhr.onerror = function() {
  alert('网络异常，请求失败！');
};

xhr.onreadystatechange = function() {
  if (xhr.readyState === 4) {
    // 区分成功和失败
    if (xhr.status >= 200 && xhr.status < 300) {
      console.log('请求成功：', JSON.parse(xhr.responseText));
    } else {
      console.log('请求失败，状态码：', xhr.status);
    }
  }
};

xhr.send();

```

## 五、jQuery Ajax 封装

原生 Ajax 代码冗余、重复度高，jQuery 对其进行了完美封装，开发更高效

### 5\.1 通用 $\.ajax 方法

```javascript
$.ajax({
  // 请求地址
  url: 'http://localhost:3000/api/data',
  // 请求方式 GET/POST/PUT/DELETE
  method: 'POST',
  // 传递参数（自动格式化）
  data: { name: '张三', age: 20 },
  // 预期响应数据格式
  dataType: 'json',
  // 是否异步（默认true）
  async: true,
  // 超时时间
  timeout: 5000,
  // 请求头配置
  headers: {
    token: 'xxxxxx'
    //Token 是后端生成的用户身份令牌，前端通过请求头 headers 携带，
    //用于接口身份验证，实现免重复登录、权限校验，是前后端分离项目的核心鉴权方式
    //(后续所有请求,请求头带上 Token后端看到合法 Token，就可以允许通过)
    //核心特点
//唯一：每个登录用户的 Token 不一样
//临时：有过期时间，过期需要重新登录
//安全：不暴露账号密码，只传令牌
  },
  // 请求成功回调
  success: function(res) {
    console.log('成功：', res);
  },
  // 请求失败回调
  error: function(err) {
    console.log('失败：', err);
  },
  //回调函数是作为参数传给另一个函数的函数(先寄存、后执行的函数)
//不是立刻执行，等待某个事件完成后执行
//Ajax 能异步，全靠回调函数接收后端数据

  // 请求完成（无论成功失败都会执行）
  complete: function() {
    console.log('请求结束');
  }
})

```

### 5\.2 简写方法

```javascript
// GET简写
$.get('接口地址', {参数}, res => { console.log(res) })

// POST简写
$.post('接口地址', {参数}, res => { console.log(res) })

```

## 六、Fetch API（现代原生异步请求）

`Fetch` 是 ES6\+ 新增的原生请求方案，基于 Promise，语法更简洁，替代老旧的 XHR

### 6\.1 基础 GET 请求

```javascript
// 默认GET请求
fetch('http://localhost:3000/api/data')
.then(res => res.json()) // 解析JSON数据
.then(data => console.log('数据：', data))
.catch(err => console.log('错误：', err))

```

### 6\.2 完整 POST 请求

```javascript
fetch('http://localhost:3000/api/add', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({ title: '测试数据' })
})
.then(res => res.json())
.then(data => console.log(data))
.catch(err => console.log(err))

```

**注意**：Fetch 只会捕获**网络错误**，404/500 接口错误不会进入 catch，需要手动判断状态码

## 七、Ajax 跨域问题

### 7\.1 什么是跨域

浏览器**同源策略**限制：协议、域名、端口号 **三者有一个不同**，即为跨域，Ajax 默认禁止跨域请求。

同源策略目的：保护用户信息安全，防止恶意网站窃取数据。

### 7\.2 常见跨域场景

- 前端 `http://localhost:8080` 请求 后端 `http://localhost:3000`（端口不同）

- 域名不同、协议不同（http/https）

### 7\.3 主流跨域解决方案

#### 7\.3\.1 CORS 后端跨域（最常用、推荐）

后端设置响应头，允许前端域名跨域访问，前端无需任何修改。

核心响应头：

```javascript
// 允许所有域名跨域（开发环境）
Access-Control-Allow-Origin: *
// 允许指定域名跨域（生产环境）
Access-Control-Allow-Origin: http://localhost:8080

```

#### 7\.3\.2 JSONP 跨域（老方案，只支持 GET）

利用 script 标签不受同源策略限制的特性实现跨域，仅支持 GET 请求，现在基本淘汰。

#### 7\.3\.3 代理跨域（前端工程化）

Vue/React 项目中配置 vite/webpack 代理，本地服务器转发请求，解决开发环境跨域。

# ES6 

## 一、ES6 变量声明：let / const（彻底淘汰 var）

### 1\.1 废弃 var的原因

ES5 只有 `var` 声明变量，存在 3 个致命 bug：

- 没有块级作用域，循环、判断会变量泄露

- 可以重复声明变量，代码混乱、容易覆盖值

- 变量提升不规范，容易出现undefined bug

### 1\.2 let 与 const 核心特性

**ES6 规范：以后声明变量只用 let / const，绝对不用 var**

|关键字|作用|是否可修改值|使用场景|
|---|---|---|---|
|**let**|声明变量|可以修改（重新赋值）|值会变的变量（计数器、接口数据、状态）|
|**const**|声明常量|不可直接修改（引用类型可改内部属性）|值永远不变的（接口地址、TOKEN、固定配置）|

### 1\.3 三大核心规则

#### 1\. 块级作用域

`let / const` 只在 `{ }` 大括号内生效（if、for、while），外部无法访问，彻底解决变量泄露。

```javascript
// 块级作用域示例
if (true) {
  let num = 10;
  const str = "ES6";
  console.log(num, str); // 10 ES6（内部可访问）
}
console.log(num); // 报错：num 未定义（外部无法访问）

```

#### 2\. 禁止重复声明

同一个作用域内，`let / const`不允许重复定义同名变量，避免代码覆盖 bug。

```javascript
var a = 1;
var a = 2; // var 允许重复声明，直接覆盖（坑）

let b = 1;
let b = 2; // 直接报错：标识符已声明（规范、安全）

```

#### 3\. 暂时性死区（无变量提升）

`let / const` 必须**先声明、后使用**，不存在变量提升，杜绝 undefined 问题。

```javascript
console.log(x); // 报错
let x = 100;

```

### 1\.4 const 重点

**const 不是完全不能改，是「内存地址不能改」**

- 基本数据类型（字符串、数字、布尔）：值不能改

- 引用数据类型（数组、对象）：**可以修改内部属性/元素**，只要不重新赋值即可

```javascript
// 基本类型：报错
const age = 18;
age = 20; // 错误！不能重新赋值

// 引用类型：正常修改
const user = { name: "张三" };
user.name = "李四"; // 合法！修改内部属性
console.log(user); // { name: "李四" }

```



## 二、异步编程：回调地狱（需要 Promise的原因）

Ajax 回调函数，多层嵌套会出现 **回调地狱**，代码又乱又难维护

### 2\.1 回调地狱的定义

多个异步请求 **必须按顺序执行**，只能嵌套写，形成「金字塔代码」。

```javascript
// 回调地狱示例（多层嵌套，极其难维护）
$.get("接口1", (res1) => {
  $.get("接口2", (res2) => {
    $.get("接口3", (res3) => {
      // 嵌套越多，代码越崩
    })
  })
})

```

### 2\.2 缺点

- 代码缩进越来越多，可读性极差

- 错误处理极其麻烦

- 无法复用、无法便捷地控制顺序

**Promise 诞生的唯一目的：解决回调地狱，扁平化异步代码**

## 三、Promise 详解

### 3\.1 Promise 是什么？

**Promise 是一个异步任务容器**，专门用来包裹异步操作（Ajax、定时器、文件读取）。

通俗理解：**承诺**，我现在干一件异步事，未来一定会有结果（成功/失败）。

### 3\.2 Promise 三种状态（不可逆）

- **pending 等待中**：任务正在执行（请求中、计时中）

- **fulfilled 成功**：任务完成，拿到结果（对应回调 success）

- **rejected 失败**：任务失败（报错、超时、跨域错误）

状态一旦从 pending 改变，**永远不会再变**。

### 3\.3 Promise 基础语法

Promise 构造函数接收一个回调，内置两个参数：

- `resolve`：成功函数，触发 `.then()`

- `reject`：失败函数，触发 `.catch()`

```javascript
// 基础 Promise 结构
const p = new Promise((resolve, reject) => {
  // 这里写异步代码：定时器 / Ajax
  let flag = true;

  if (flag) {
    resolve("请求成功的数据"); // 成功结果
  } else {
    reject("请求失败了"); // 失败原因
  }
});

// 接收结果
p.then(res => {
  console.log("成功：", res);
}).catch(err => {
  console.log("失败：", err);
})

```

### 3\.4 Promise 链式调用（解决回调地狱）

核心：**\.then\(\) 可以无限链式调用，代替嵌套**，代码从上到下扁平化执行。

```javascript
// 模拟顺序执行多个异步任务（无嵌套）
new Promise((resolve) => resolve(1))
.then(res => {
  console.log(res);
  return 2; // 返回值传给下一个 then
})
.then(res => {
  console.log(res);
  return 3;
})
.then(res => console.log(res))
.catch(err => console.log(err));
//如果在任意一个 then 里写 reject() 或者报错，后面的 then 全部不执行，直接跳进 catch。
```

对比回调嵌套：**彻底扁平化，层级不变，好维护**

### 3\.5 Promise 封装 Ajax

**把原生 Ajax 封装成 Promise，** 告别回调，适配后续 async/await

```javascript
// 封装 GET 请求
function getApi(url) {
  return new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest();
    xhr.open("GET", url, true);
    xhr.onreadystatechange = function() {
      if (xhr.readyState === 4) {
        if (xhr.status === 200) {
          resolve(JSON.parse(xhr.responseText)); // 成功
        } else {
          reject("请求失败"); // 失败
        }
      }
    }
    xhr.send();
  })
}

// 调用
getApi("http://localhost:3000/api/data")
.then(res => console.log("数据：", res))
.catch(err => console.log(err))
```

## 四、终极异步方案：async / await（ES7 基于 Promise）

### 4\.1 核心作用

- 基于 Promise 封装，语法更简洁

- **await 可以等待异步任务执行完毕**，再执行下一行代码

- 彻底消灭回调、消灭链式 \.then\(\)

### 4\.2 两个核心关键字

1. **async**：修饰函数，`async 函数()`，代表这个函数内部**可以写 await**

2. **await**：**等待 Promise 执行完成**，直接拿到成功结果

### 4\.3 基础语法

```javascript
// 必须搭配 async + await
async function getData() {
  // await 等待 Promise 结束，直接拿到 res
  const res = await getApi("http://localhost:3000/api/data");
  console.log("最终数据：", res);
}

// 调用函数
getData();

```

### 4\.4 顺序执行多个接口

多个异步接口需要按顺序执行，async/await 在这种场景下十分便捷

```javascript
async function getAllData() {
  // 先执行接口1，完成后再执行接口2
  const res1 = await getApi("接口1");
  console.log(res1);

  const res2 = await getApi("接口2");
  console.log(res2);
}
getAllData();

```

### 4\.5 错误处理

await 报错会直接终止代码，必须用 **try / catch** 捕获异常

```javascript
async function getData() {
  try {
    // 尝试执行异步代码
    const res = await getApi("错误接口地址");
    console.log(res);
  } catch (err) {
    // 捕获所有失败：404、500、跨域、超时
    console.log("请求出错：", err);
  }
}
getData();

```

## 五、全套异步方案进化史

看懂进化史，彻底打通所有异步逻辑

1. **原生回调函数**：最简单，缺点 = 回调地狱、嵌套爆炸

2. **Promise 链式调用**：解决嵌套，缺点 = 过多 then 依然繁琐

3. **async / await**：终极方案，同步写法、异步逻辑

