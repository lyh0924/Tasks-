 [网页链接](https://lyh0924.github.io/geek-web/)

 ```
 <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Geek组旧版招新网站复刻</title>
    <style>
        *{
            margin:0;
            padding:0;
            box-sizing:border-box;/*若不加这个padding和border会往外撑，把盒子撑大，使最终大小跟设定的不一样*/
        }
        ul,
        li{list-style:none;}
        body{
             overflow-x:hidden;/*禁止页面出现横向滑动条，防止内容超出屏幕导致页面左右滑动*/
        }
        /*平滑效果*/
        html{
            scroll-behavior: smooth;
        }
        a{
            text-decoration: none;
            display:block;/*变成块状元素独占一行，可以设置宽高*/
        }
        /*顶部导航栏*/
        .nav-top{
            background-color:rgba(255, 213, 0, 0.9);
            width: 1200px;
            height:40px;
            border-radius:15px;
            position:fixed;/*固定导航栏的通用写法*/
            top:10px;/*使用top等性质，盒子必须要有position属性*/
            left:50%;/*margin:0 auto起到居中效果，对于定位盒子（position）是无效的，对于还没有定位的盒子中的有宽度的块级盒子有效*/
            margin-left:-600px;/*利用left和margin-left让盒子居中*/
           /*更优化的居中写法：left:50%  transform:translateX(-50%);*/
            z-index:999;
            display:flex;
            justify-content: center;
            align-items:center;
        }
        /* 小盒子 */
        .nav-top .item{
            width:240px; 
             height:40px; 
            border-radius: 15px;
            transition:all 0.3s ease;
            font-family: Arial, Helvetica, sans-serif;
            font-size:20px;
            color:white;
            line-height: 40px;
            text-align:center;
        }
        /* 小盒子：newthread */
        .nav-top .item1{
            width:240px; 
             height:40px; 
            border-radius: 15px;
            transition:all 0.3s ease;
            font-family: Arial, Helvetica, sans-serif;
            font-size:20px;
            color:rgba(128,137,144,0.9);
            line-height: 40px;
            text-align:center;
        }
        .nav-top .item:hover{
            background-color:rgba(251, 129, 85, 0.9);
            color:rgba(128,137,144,0.9);
        }
        .nav-top .item1:hover{
            background-color:rgba(251, 129, 85, 0.9);
            color:white;
        }
        /* 让introduction成为二维码的父盒子，保证二维码相对它定位，且子相父位，所以用relative */
        .introduction-father{
            position:relative;
              display:inline-block;/*具有行内块元素的性质，都在一行上且可以设置宽高 */
             width:240px; 
             height:40px; 
            border-radius: 15px;
            transition:all 0.3s ease;
            font-family: Arial, Helvetica, sans-serif;
            font-size:20px;
            color:white;
            line-height: 40px;
            text-align:center;
        }
        .introduction-father a{
            color:white;
            display:block;
            width:100%;
            height:100%;
        }
        /* 二维码卡片 */
        .code-card{
            display:none;/*让二维码不能被看见，要等鼠标经过才能看见*/
            position:absolute; /*让二维码悬浮在按钮下方*/
            top:100%;/*紧贴按钮底部*/
            left:50%;
            margin-left:-70px;
            z-index:999;
            background-color: white;
            padding-left: 10px;
            padding-right: 10px;
            /* padding-bottom: 5px; */
           border:3px solid rgba(251, 129, 85, 0.9);
           border-radius: 10px;
            text-align: center;
            min-width:120px;
            margin-top: 10px;
            pointer-events: auto!important;/*让二维码能接受鼠标事件*/
        }
         .introduction-father:hover{
            background-color:rgba(251, 129, 85, 0.9)!important;
        } 
        .introduction-father:hover a{
            color:rgba(128,137,144,0.9)!important;
        }
        .introduction-father:hover .code-card,
        .code-card:hover{
            display: block!important;
        }
        /* 二维码图片样式 */
        .code-img{
            width:110px;
            height:155px;
            display:block;
            margin:0 auto 10px;
        }
        /* 二维码下方文字说明样式 */
        .code-decs{
            font-size:14px;
            font-weight:450px;
            color:#333;
        }
        .first-page{
            background-image: url(./images/background_Homepage.png);
           width:1200px; 
            min-height: 100vh;
            position: relative;
            left:50%;
            margin-left: -600px;
            margin-top:60px;
            bottom:5px;
             scroll-margin-top: 60px;
            /* background-position: center;  */
            background-size: cover;
            background-repeat: no-repeat;
            display: flex;
             align-items: center;
        }
        /* geek大图标 */
        .geek-big{
            /* background-image: url(./images/decoration_Geek.png); */
            width: 400px;
            height:200px;          
           position:absolute;
            top:80px;
          
            left:50%;/*margin:0 auto对于定位盒子是无效的*/
            margin-left:-200px;/*利用left和margin-left让盒子居中*/
            z-index:998;
            display:flex;
            justify-content: center;
            align-items:center;
        }
        .geek-big:hover{
            transform:scale(1.38);
            transition: all 0.5s ease;
        }
        /* introduction */
        .decoration{
            width:100%;
            height:auto;
            display:flex;
            position:relative;
            justify-content: center;
            align-items:center;
            background-repeat:no-repeat;
            background-position: center;
            /* margin:10px; */
            padding:40px;
            background-image: url(./images/decoration_Transition.png);
            background-size: 100% auto;
        }
        .card{
            display:flex;
            flex-direction:column;
            /* gap:40px; */
            margin-bottom:20px;
            margin-top: 20px;
            align-items:center;
        }
        /* .card:hover{
            transform: scale(1.1);
            transition:all 0.3s ease;
        } */
        /* 文字左，图片右 */
        .card-type{
            width:1000px;
            border:3px solid grey;
            border-radius:10px;
            padding:25px 18px;
            box-shadow:0 4px 9px;
            display:flex;
            max-height:426px;
            /* margin-bottom: 5px; */
            /* align-items:center;
            gap:30px; */
        }
        .card-type:hover{
             transform: scale(1.04);
            transition:all 0.3s ease;
        }
        .card-word{
            flex:1.2;
        }
        .card-title1{
            font-size:37px;
            color:black;
            font-weight:700;
            margin-bottom: 25px;
        }
        .card-title2{
            font-size:33px;
            /* color:rgb(34, 145, 255); */
            font-weight:700;
            margin-bottom:30px;
            letter-spacing: 0.5px;
        }
        .card-title3{
            font-size:20px;
            color:black;
            font-weight:550;
            line-height:23px;
            letter-spacing:0.8px;
        }
        .card-img{
            flex:0.8;
            display: flex;
            align-items:center;
            justify-content: center;
        }
        .card-img img{
            max-width:100%;
            height: auto;
        
            display:block;
            max-height:360px;
            object-fit:contain;
        
        }
        .left{
            display:flex;
            align-items:center;
            gap:30px;
        }
         /* 文字右，图片左 */
        .right{
             display:flex;
            align-items:center;
            gap:30px;
            flex-direction: row-reverse;
        }
        .animation{
            transition: transform 0.3s ease;
            transform-origin: center;
        }
        .animation:hover{
            transform:rotate(-15deg);
        }
        .animation1{
            transition: transform 0.3s ease;
            transform-origin: center;
        }
        .animation1:hover{
            transform:rotate(15deg);
        }
        .about{
            display:flex;
            border:solid grey 7px;
            width:1100px;
            height:600px;
            position:relative;
            flex-direction:column;
            border-radius:20px;
            background-color: rgba(255, 255, 250, 0.3);
            text-align: center;
            left:50%;
            margin-left:-550px;
            margin-top:65px;
            align-items: center;
            /* justify-content: center; */
          padding:0 100px;
          /* margin:-20px; */
          gap:30px;
          box-sizing:border-box;
        }
         .about>div{
           display:flex;
          
           gap:120px;

        } 
        .about-us-title{
            font-size:60px;
            margin-bottom:10px;

            text-align:center;
            color:grey;
            font-weight: 400;
        }
        .purple{
            width:155px;
            height:295px;
            border-radius:15px;
            border:solid purple 5px;
            display:flex;
            overflow: hidden;
            flex-direction: column;
            align-items:center;
            padding:10px 8px;
            gap:15px;
            box-sizing:border-box;
        }
        .purple img{
            width:auto;
            max-width:100%;
            max-height:100px;
            height:auto;
            object-fit:contain;
            display:block;
            flex-shrink: 0;
            margin-bottom: 11px;
        }
        .purple .text{
            font-size:16px;
            text-align:left;
            line-height:1.4;
            margin:0;
            flex:1;
            font-weight: 480;
        }
        .purple1{
            width:165px;
            height:320px;
            border-radius:15px;
            border:solid purple 5px;
            display:flex;
            overflow: hidden;
             flex-direction: column;
            align-items:center;
            padding:10px 8px;
            gap:15px;
            box-sizing:border-box;
        }
        .purple1 .text{
            font-size:16px;
            text-align:left;
            line-height:1.4;
             margin:0;
            flex:1;
             font-weight: 480;
        }
        .purple1 img{
            width:auto;
            max-width:100%;
            max-height:100px;
            height:auto;
            object-fit:contain;
            display:block;
            flex-shrink: 0;
            margin-bottom: 11px;
        }
        .purple:hover{
            transform: scale(1.08);
            transition: all 0.4s ease;
        }
         .purple1:hover{
            transform: scale(1.08);
            transition: all 0.4s ease;
        }
        .corner{
            width:200px;
            height:200px;
            object-fit:contain;
            position:absolute;
        }
        .top-left{
            top:-80px;
            left:-50px;
            
            transform:scaleX(-1);
        }
        .top-right{
            
            top:-80px;
            right:-50px;
        }
        .bottom-left{
            
            bottom:-80px;
            left:-50px;
            transform:scaleX(-1)scaleY(-1);
        }
        .bottom-right{
           
            bottom:-80px;
            right:-50px;
            transform:scaleY(-1);
        }
        .butterfly{
            bottom:33px;
            right:25px;
        }
        .butterfly:hover{
            transform:scale(0.8);
            transition:all 0.3s ease;
            transform: translateY(7px);
        }
        .contact{
            border:rgb(1, 129, 114) solid 7px;
            border-radius: 20px;
            width:1100px;
            height:600px;
            left:50%;
            margin-left: -550px;
            display:flex;
            position:relative;
            margin-top:65px;
            text-align: center;
            justify-content: center;
           /* gap:18px; */
        }
        .contact-photo1{
            top:-50px;
            left:-63px;
            width:355px;
            height:355px;
            object-fit:contain;
            position:absolute;
           
        }
        .contact-photo2{
            left:335px;
            top:30px;
            object-fit:contain;
            position:absolute;
            width:50px;
            height:50px;
        }
        .contact-photo3{
            top:-20px;
            right:-220px;
            position:absolute;
            width:550px;
            height:645px;
            object-fit:contain;
         
        }
        .contact-photo4{
            left:-18px;
            bottom:-20px;
            object-fit:contain;
            position:absolute;
            width:60px;
            height:60px;
        }
        .contact-photo5{
            width:410px;
            height:410px;
            position:absolute;
            object-fit: contain;
            bottom:-132px;
            right:105px;
            z-index: 1;
        }
        .contact-title{
            font-size:49px;
            font-weight: 400;
           
            color:rgb(76, 74, 74);
           position:absolute;
           top:18px;
           
        }
        .contact-text{
            font-size:26px;
            font-weight:400;
            letter-spacing:0.1px;
           width:565px;
           text-align:left;
            /* gap:18px;应该写在父元素里面 */
            /* position:absolute; absolute会导致文档脱离正常流*/
          white-space: nowrap;

        }
        .contact-ps{
            font-size:18px;
            font-weight:400;
            letter-spacing:0.1px;
           width:565px;
           text-align:left;
           color:rgb(108, 107, 107);
           line-height:23px;
        }
        .contact-ul{
            display:flex;
            flex-direction:column;
            gap:20px;
            padding:0;
            margin:0;
            list-style:none;
            top:130px;
            
         position:absolute;
         left:210px;
        }
        .contact-green-box{
            display:flex;
            gap:30px;
            position:absolute;
            bottom:60px;
           left:50%;
           margin-left: -250px;
        }
        .contact-green{
            /* border:green solid 1px; */
            border-radius:10px;
            background-color: green;
            color:white;
            width:120px; 
            height:29px;
             line-height: 24px;
            box-shadow:0 4px 10px rgba(1,129,114,0.3);
           text-shadow: 0 1px 3px rgba(0,0,0,o.3);
           z-index: 10;
        }
        .contact-green:hover{
            transform: scale(1.1);
            transition: all 0.3s ease;
        }
      .qa-container {
    width: 100%;
    max-width: 1100px;
    min-height: 350px;
    margin: 65px auto 80px;
    border: #2196f3 solid 9px;
    border-radius: 16px;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    position: relative;
    overflow: hidden;
    z-index: 1;
    background-color: #8dc6ff;
}
.qa-background {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 800px;
    object-fit: cover;
    z-index: 1;
    user-select: none;
    pointer-events: none;
}
.qa-content {
    position: relative;
    z-index: 2;
    padding: 30px 60px 40px;
    text-align: center;
}
.qa-title {
    font-size: 32px;
    color: #111827;
    margin: 0 0 25px 0;
    font-weight: bold;
}
.qa-list {
    max-width: 100%;
    margin: 0 auto;
    text-align: left;
}
.qa-item {
    margin-bottom: 15px;
}
.qa-q {
    font-size: 20px;
    color: #111827;
    font-weight: 500;
    cursor: pointer;
    transition: all 0.3s ease;
    display: inline-block;
    line-height: 1.5;
}
.qa-q:hover {
    color: #1e40af;
    transform: translateX(8px) scale(1.05);
}
.qa-a {
    max-height: 0;
    overflow: hidden;
    transition: max-height 0.4s ease,padding 0.4s ease;
    background-color: rgba(255,255,255,0.7);
    border-radius: 12px;
    margin-top: 10px;
    padding: 0 20px;
    font-size: 16px;
    color: #374151;
    line-height: 1.7;
    box-sizing: border-box;
}
.qa-item.active .qa-a {
    max-height: 300px;
    padding: 20px;
}
       .footer {
  background-color: rgba(188, 185, 185, 0.262);
  color: black;
  text-align: center;
  padding: 20px 10px;
  font-size: 10px;
  font-weight: 500;
  margin-top: 60px; /* 和上面的内容拉开距离 */
  border:none;
  border-top:3px solid rgba(188, 185, 185, 0.262);
  width:100vw;
}
.footer p {
  margin: 0;
  line-height: 1.6;
}

        .back{
            width:40px;
            height:32px;
            border-radius:8px;
            background-color: white;
            border:solid 2px black;
            right:7px;
            bottom: 30px;
            position:fixed;

        } 
    </style>
</head>
<body>
    <!-- 顶部导航栏 -->
    <div class="nav-top">
    <div class="introduction-father">
        <a href="#introduction">Introduction</a>
        <div class="code-card">
        <img src="./images/qrcode_1699620268564.jpg" alt="加入GEEK的二维码图片" class="code-img">
        <div class="code-decs">极客扫码加入Geek</div>
    </div>
    </div>
         <a href="#About" class="item">About US</a>  <!-- /*在锚点链接中空格是非法字符会导致匹配失败*/ -->
        <a href="https://new-thread.com/" target="_blank" class="item1">NewThread</a>
        <a href="#contact" class="item">contact US</a>
        <a href="#qa" class="item">Q&A</a>
    </div>
    <!-- 首页 -->
    <section class="first-page">
        <!-- <div class="geek-big"></div> -->
         <img src="./images/decoration_Geek.png" alt="geek" class="geek-big geek-big.hover">
        <!-- <img src="../geek/复刻招新网站要求点/images/decoration_Transition.png"> -->
    </section>
    <!-- 返回顶部 -->
        <a class="back" href="#top">back</a>
    

     <!-- intruduction -->
    <div class="decoration">
    <h3 id="introduction" style="font-weight:700;font-size:37px;color:rgb(16, 72, 242);margin:70px auto;text-align: center;width:fit-content;position:relative;">Introduction</h3>
    <!-- <img src="../geek/复刻招新网站要求点/images/decoration_Transition.png"> -->
    </div>

    <!-- 程序员 -->
    <div class="card">
     <div class="card-type left">
        <div class="card-word">
            <h3 class="card-title1">&nbsp;&nbsp;开发程序猿</h3>
            <p class="card-title2" style="color:rgb(34, 145, 255);">&nbsp;&nbsp;"Stay Hungry,Stay Foolish"</p>
            <p class="card-title3">前端：前端开发是创建Web或app视觉界面呈现给用户的过程通过HTML,CSS及JavaScript以及衍生出来的各种技术、框架、解决方案,实现互联网产品的用户界面交互。
                <br><br>
                后端：通常也称服务器端开发。不对用户显示,负责处理前端的请求，进行逻辑处理和数据交互。 客户端: 移动应用开发是为了小型、无线计算设备编写软件的流程和程序的集合，例如智能手机或平板电脑。
            </p>
     </div>  
     <div class="card-img">
        <img src="./images/Geek_Programmer.png" class="animation">
     </div>
   </div>
   <div>
    
   <!-- 产品经理 -->
     <div class="card">
     <div class="card-type right">
        <div class="card-word">
             <h3 class="card-title1"><!--&nbsp;&nbsp; -->产品经理</h3>
            <p class="card-title2" style="color:rgba(226, 142, 232, 0.791);">"好的软件的特征是,明明没用过,但总觉得用过似的。"</p>
            <p class="card-title3">PM是针对某一项或是某一类的产品进行规划和管理的人员。 PM需要拥有缜密的产品逻辑思维，研究用户心理，负责产品的整个生命周期。 PM参与产品的UI和交互设计，为设计和开发确定产品原型，能够将产品变得有个性,操作变得舒适简单、自由。 PM需要一定的文档能力和沟通能力，能够在团队合作的过程中跟各个角色进行有效沟通。
            </p>
     </div>  
     <div class="card-img">
        <img src="./images/Geek_PM.png" class="animation1">
     </div>
     </div>
     </div>

     <!-- 游戏开发 -->
    <div class="card">
     <div class="card-type left">
        <div class="card-word">
            <h3 class="card-title1">&nbsp;&nbsp;游戏开发</h3>
            <p class="card-title2" style="color:rgb(67, 241, 218);white-space: nowrap;">&nbsp;&nbsp;"TECH OTAKUS SAVE THE WORLD"</p>
            <p class="card-title3">对游戏开发的热爱和追求，使我们相聚于此。 涉及计算机图形学的学习，我们使用物理模拟引擎Unity开发我们所追求的世界，一个故事，一个角色，在我们的世界里改变现实，创造新的可能，我们参与，我们改变，我们创造...
            </p>
     </div>  
     <div class="card-img">
        <img src="./images/Geek_Game.png" class="animation">
     </div>
   </div>
   <div>

    <!-- 安全 -->
     <div class="card">
     <div class="card-type right">
        <div class="card-word">
             <h3 class="card-title1"><!--&nbsp;&nbsp; -->安全</h3>
            <p class="card-title2" style="color:pink;">"路漫漫其修远兮，非大毅力者不能"</p>
            <p class="card-title3">我们主要学习Web安全和二进制安全。在Web安全中我们将学习和实践Web漏洞挖掘技术，也将探索和讨论Web安全实践的方法。在二进制安全中我们专注于分析和防御与计算机程序、系统相关的威胁，同时实践漏洞分析和修补。耐心和钻研缺一不可。
     </div>  
     <div class="card-img">
        <img src="./images/Geek_security.png" class="animation1">
     </div>
     </div>
     </div>

     <!-- About US -->

      <div id="About" class="about">
        <h2 class="about-us-title">About Us</h2>
         <img src="./images/decoration_Decoration.png" class="corner top-left">
      <img src="./images/decoration_Decoration.png" class="corner top-right">
      <img src="./images/decoration_Decoration.png" class="corner bottom-left">
      <img src="./images/decoration_Decoration.png" class=" corner bottom-right"> 
      <img src="./images/decoration_Butterfly.png" title="保持好奇心！" class="corner butterfly">
          <div>
        <div class="purple">
            <img src="./images/about_Speech.png">
            <div class="text">每周我们会举行一次技术例会，用来汇报我们的学习内容，供成员之间交流学习。</div>
        </div>
        <div class="purple1">
            <img src="./images/about_Diversity.png">
            <div class="text">多元化是我们的特色。在这里，你可以拥有多种方向选择，前后端、安全、AI、产品/设计、游戏等。</div>
        </div>
        <div class="purple">
            <img src="./images/about_Time.png">
            <div class="text">耐心、毅力是我们必备的品质，每周我们会至少花30小时在实验室中。以保证技术的精进。</div>
        </div>
      </div>
      </div> 
     
     <!-- contact us -->
    <div class="contact">
        <img src="./images/decoration_Chameleon.png" class="contact-photo5">
        <img src="./images/decoration_Ladybug.png" class="contact-photo4">
        <img src="./images/decoration_Leaves.png" class="contact-photo2">
        <img src="./images/decoration_Tree.png" class="contact-photo3">
        <img src="./images/decoration_TreeWithSometing.png" class="contact-photo1">
        <div id="contact" class="contact-title">Contact Us</div>
            <ul class="contact-ul">
                <li class="contact-text">•热爱计算机，具有geek精神，喜欢DIY，动手能力较强</li>
                <li class="contact-text">•有编程/算法/硬件基础为佳(有作品可附上)</li>
                <li class="contact-text">•有足够的空余时间，热爱思考，对事物有自己的见解</li>
                <li class="contact-ps">ps:非新思路统招只有通过发送邮件自我介绍后，收到邮件回执后才会被允许进群,在读学生, 都可邮件到newthread_geek@outlook.com报名加入.(信中需备注个人基本信息以及意向方向,此招新活动为长期招新)</li>
            </ul>
        <div class="contact-green-box">
        <a href="#" class="contact-green">QQ-Group</a>
        <a  herf="javasript:;" class="contact-green" onclick="copyEmail()">E-mail</a>
        <a href="https://github.com/" class="contact-green" target="_blank">Github</a>
        </div>
    </div>

       <!-- Q&A -->
   <div id="qa" class="qa-container">
        <img src="./images/background_QA.png" alt="QA背景图" class="qa-background">
        <div class="qa-content">
            <h2 class="qa-title">More Questions</h2>
            <div class="qa-list">
                <div class="qa-item">
                    <div class="qa-q">1.什么是Geek(极客)？Geek精神又是什么？</div>
                    <div class="qa-a">拥有好奇之心，改变之力，爱钻研，能折腾。</div>
                </div>
                <div class="qa-item">
                    <div class="qa-q">2.招新是安排在什么时间？</div>
                    <div class="qa-a">按照惯例，正式招新时间是在9月下旬~10月上旬，不过今年会有一些改动，笔试地 点一般在9号教学楼。 如果想要了解我们，可以加入我们的QQ群，招新具体的安排/变动会在招新群通知。</div>
                </div>
                <div class="qa-item">
                    <div class="qa-q">3.我们有考核吗？考核流程是怎样的呀？</div>
                    <div class="qa-a">嗯...我们一共有一轮笔试和两轮面试。权衡技术、经验和学习能力，第一轮是一些视野性的题目，淘汰率并不高。第二轮单独面试， 根据你的笔试提出技术相关的问题、兴趣爱好、个人看法。最后一轮群面，首先问及时间分 配上的问题，其次也会向你提出各种奇怪的问题。这一轮中许多题目其实并不难，也无标准答案，重在考察同学们在压力下的逻辑思维。全部通过成为预备成员啦。</div>
                </div>
                <div class="qa-item">
                    <div class="qa-q">4.考核是怎样的形式？</div>
                    <div class="qa-a">在考核期间每人会拥有一位'长者'带你入门，学习技术与知识，交流经验与想法。完成每周的新人任务后再进行一次考核筛选 后就可以成为Geek组正式成员啦！在考核期必须满足每周30个小时在实验室哦,所以考核期也不可以懈怠哦！</div>
                </div>
                <div class="qa-item">
                    <div class="qa-q">5.进入Geek组之后都有什么福利呢？</div>
                    <div class="qa-a">一对一的新人指引，每一个成员都有会一个mentor, 带你初入门槛，与你一同成长，组内管理较宽松,在尊重其他人的前提下可以尽情发挥自己的个性。 打破平淡，与同样疯狂的人把疯狂的idea实现，磨砺耐性、培养思维、成就梦想。Lab设备/网络资源充足，闲暇之余也有组织活动。更有许多的故事等你来听~</div>
                </div>
                <div class="qa-item">
                    <div class="qa-q">6.进入团队会影响我的日常学习吗？</div>
                    <div class="qa-a">你要知道大学是一个可以自由安排自己学习生活的地方。如果你想在上课之余充实自己、激励自己，最好的方法就是和比自己更优秀的人在一起。团队不缺优秀的 人，而我们也期待同样优秀的你，让我们一起前进！小组里也有不少保研, 考研的前辈们, 大部分都能找到一个平衡点, 而且团队的经历对你日后读研, 工作都大有裨益。</div>
                </div>
                <div class="qa-item">
                    <div class="qa-q">7.老师以及学长学姐们的期望是什么?</div>
                    <div class="qa-a">“我们希望你有很强的自学能力，同时关注新事物、新技术，喜欢挑战，逻辑性强，善于和各种文化的人合作.“每个人都可以做自己想做的事情，每个人的方向不一样。 如果你想做产品或有不错的 idea，那么就可以找志同道合的人一起合作。”</div>
                </div>
            </div>
    </div>
</div>
<footer class="footer">
  <p>[prentending this is true]<br>Copyright©2002-2022 itaweya.github.io All Right Reserved 备案号：?????</p >
</footer>
        
<script>
        const qaItems = document.querySelectorAll('.qa-item');
        qaItems.forEach(item => {
            const question = item.querySelector('.qa-q');
            const answer = item.querySelector('.qa-a');
            question.addEventListener('click', () => {
                item.classList.toggle('active');
            });
        });
    </script>
    <script>
    // 定义复制邮箱的函数
    function copyEmail() {
        // 这里填目标邮箱
        const email = " newthread_geek@outlook.com";
        
        // 创建一个临时的 input 元素用于复制
        const tempInput = document.createElement("input");
        tempInput.value = email;
        document.body.appendChild(tempInput);
        tempInput.select(); // 选中内容
        document.execCommand("copy"); // 执行复制命令
        document.body.removeChild(tempInput); // 移除临时元素
        
        // 弹出提示框
        alert("Geek的邮箱已复制到剪贴板！\n" + email);
    }
</script>
</body>
</html>
```
