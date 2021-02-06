# 2020前端面试(一面面试题）

https://zhuanlan.zhihu.com/p/84212558

都说金9银10，节前自己也去面试了几家公司，幸而都收到了offer。如今已经办理好了离职手续，闲来有空，整理一番，希望对各位节后找工作有帮助。

说在前面，我的答案仅供参考。答案有不全或有偏颇之处，欢迎各位在评论区补充及指正。

一面都比较偏基础，大部分题目都会，即使不会也似曾相识，都能说上几句。但为什么有些人能过有些人过不了，这就是考查你的基础知识是否全面且扎实。会是应该的，但你的答案一定要详细并且有些题要说出多种答案。这就需要各位平常的积累了



### CSS

### 盒模型的计算

```css
/*以下盒模型的 offsetWidth 是多少*/
#box {
  width: 100px;
  padding: 10px;
  border: 1px solid #ccc;
  margin: 10px;
}
/*
页面宽度: 122px
offsetWidth=(内容宽度 + 内边距 + 边框),无外边距
box-sizeing: border-box;
*/
```

### 如何实现一个扇形

```css
#sector {
  width: 0;
  height: 0;
  border-width: 50px;
  border-style: solid;
  border-color: red transparent transparent;
  border-radius: 50px;
}


```

### margin 纵向重叠问题

```html
<style>
p{
  font-size:16px;
  line-height: 1;
  margin-top: 10px;
  margin-bottom: 15px;
}
</style>
<p>AAA</p>
<p></p>
<p></p>
<p></p>
<p>BBB</p>
<!-- 如上代码,AAA 与 BBB 这间的距离是多少? --> 
<!-- 答案: 15px -->
```

- 相邻元素的margin-top 和margin-bottom 会发生重叠
- 空白内容的<p></p>也会发生重叠

### 对 margin 的top right bottom left 设置负值 会有什么效果?

- margin-top left 是平移元素自身
- margin-right bottom 是平移其他元素
- 负值朝相反方向移动

### 什么是 BFC?

块格式化上下文

一个独立渲染区域, 内部元素的渲染不会影响边界以外的元素

> > 
> > BFC(Block formatting context)直译为"块级格式化上下文"。它是一个独立的渲染区域，只有Block-level box参与， 它规定了内部的Block-level Box如何布局，并且与这个区域外部毫不相干。
>
> 在解释什么是BFC之前，我们需要先知道Box、Formatting Context的概念。
>
> ###### Box：css布局的基本单位
>
> Box 是 CSS 布局的对象和基本单位， 直观点来说，就是一个页面是由很多个 Box 组成的。元素的类型和 display 属性，决定了这个 Box 的类型。 不同类型的 Box， 会参与不同的 Formatting Context（一个决定如何渲染文档的容器），因此Box内的元素会以不同的方式渲染。让我们看看有哪些盒子：
>
> - block-level box:display 属性为 block, list-item, table 的元素，会生成 block-level box。并且参与 block fomatting context；
> - inline-level box:display 属性为 inline, inline-block, inline-table 的元素，会生成 inline-level box。并且参与 inline formatting context；
> - run-in box: css3 中才有， 这儿先不讲了。
>
> ###### Formatting Context
>
> Formatting context 是 W3C CSS2.1 规范中的一个概念。它是页面中的一块渲染区域，并且有一套渲染规则，它决定了其子元素将如何定位，以及和其他元素的关系和相互作用。最常见的 Formatting context 有 Block fomatting context (简称BFC)和 Inline formatting context (简称IFC)。
>
> > ```
> > BFC是一个独立的布局环境，其中的元素布局是不受外界的影响，并且在一个BFC中，块盒与行盒（行盒由一行中所有的内联元素所组成）都会垂直的沿着其父元素的边框排列。
> > ```
>
> ### BFC的布局规则
>
> - 内部的Box会在垂直方向，一个接一个地放置。
> - Box垂直方向的距离由margin决定。属于**同一个**BFC的两个相邻Box的margin会发生重叠。
> - 每个盒子（块盒与行盒）的margin box的左边，与包含块border box的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。
> - BFC的区域不会与float box重叠。
> - BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。
> - 计算BFC的高度时，浮动元素也参与计算。
>
> ### 如何创建BFC
>
> - 1、float的值不是none。
> - 2、position的值不是static或者relative。
> - 3、display的值是inline-block、table-cell、flex、table-caption或者inline-flex
> - 4、overflow的值不是visible
>
> ### BFC的作用
>
> ###### 1.利用BFC避免margin重叠。
>
> 一起来看一个例子：
>
> ```
> <!DOCTYPE html>
> <html lang="en">
> <head>
>     <meta charset="UTF-8">
>     <meta name="viewport" content="width=device-width, initial-scale=1.0">
>     <meta http-equiv="X-UA-Compatible" content="ie=edge">
>     <title>防止margin重叠</title>
> </head>
> <style>
>     *{
>         margin: 0;
>         padding: 0;
>     }
>     p {
>         color: #f55;
>         background: yellow;
>         width: 200px;
>         line-height: 100px;
>         text-align:center;
>         margin: 30px;
>     }
> </style>
> <body>
>     <p>看看我的 margin是多少</p>
>     <p>看看我的 margin是多少</p>
> </body>
> </html>
> 123456789101112131415161718192021222324252627
> ```
>
> 页面生成的效果就是这样的：
> ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190323155704915.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NpbmF0XzM2NDIyMjM2,size_16,color_FFFFFF,t_70)
> 根据第二条，属于同一个BFC的两个相邻的Box会发生margin重叠，所以我们可以设置，两个不同的BFC，也就是我们可以让把第二个p用div包起来，然后激活它使其成为一个BFC
>
> ```
> <!DOCTYPE html>
> <html lang="en">
> <head>
>     <meta charset="UTF-8">
>     <meta name="viewport" content="width=device-width, initial-scale=1.0">
>     <meta http-equiv="X-UA-Compatible" content="ie=edge">
>     <title>防止margin重叠</title>
> </head>
> <style>
>     *{
>         margin: 0;
>         padding: 0;
>     }
>     p {
>         color: #f55;
>         background: yellow;
>         width: 200px;
>         line-height: 100px;
>         text-align:center;
>         margin: 30px;
>     }
>     div{
>         overflow: hidden;
>     }
> </style>
> <body>
>     <p>看看我的 margin是多少</p>
>     <div>
>         <p>看看我的 margin是多少</p>
>     </div>
> </body>
> </html>
> 1234567891011121314151617181920212223242526272829303132
> ```
>
> ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190323160150540.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NpbmF0XzM2NDIyMjM2,size_16,color_FFFFFF,t_70)
>
> ###### 2.自适应两栏布局
>
> 根据：
>
> - 每个盒子的margin box的左边，与包含块border box的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。
>
> ```
> <!DOCTYPE html>
> <html lang="en">
> <head>
>     <meta charset="UTF-8">
>     <meta name="viewport" content="width=device-width, initial-scale=1.0">
>     <meta http-equiv="X-UA-Compatible" content="ie=edge">
>     <title>Document</title>
> </head>
> <style>
>     *{
>         margin: 0;
>         padding: 0;
>     }
>     body {
>         width: 100%;
>         position: relative;
>     }
>  
>     .left {
>         width: 100px;
>         height: 150px;
>         float: left;
>         background: rgb(139, 214, 78);
>         text-align: center;
>         line-height: 150px;
>         font-size: 20px;
>     }
>  
>     .right {
>         height: 300px;
>         background: rgb(170, 54, 236);
>         text-align: center;
>         line-height: 300px;
>         font-size: 40px;
>     }
> </style>
> <body>
>     <div class="left">LEFT</div>
>     <div class="right">RIGHT</div>
> </body>
> </html>
> 1234567891011121314151617181920212223242526272829303132333435363738394041
> ```
>
> 页面：
>
> ![在这里插入图片描述](https://img-blog.csdnimg.cn/2019032316073845.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NpbmF0XzM2NDIyMjM2,size_16,color_FFFFFF,t_70)
>
> 又因为：
>
> - BFC的区域不会与float box重叠。
>
> 所以我们让right单独成为一个BFC
>
> ```
> <!DOCTYPE html>
> <html lang="en">
> <head>
>     <meta charset="UTF-8">
>     <meta name="viewport" content="width=device-width, initial-scale=1.0">
>     <meta http-equiv="X-UA-Compatible" content="ie=edge">
>     <title>Document</title>
> </head>
> <style>
>     *{
>         margin: 0;
>         padding: 0;
>     }
>     body {
>         width: 100%;
>         position: relative;
>     }
>  
>     .left {
>         width: 100px;
>         height: 150px;
>         float: left;
>         background: rgb(139, 214, 78);
>         text-align: center;
>         line-height: 150px;
>         font-size: 20px;
>     }
>  
>     .right {
>         overflow: hidden;
>         height: 300px;
>         background: rgb(170, 54, 236);
>         text-align: center;
>         line-height: 300px;
>         font-size: 40px;
>     }
> </style>
> <body>
>     <div class="left">LEFT</div>
>     <div class="right">RIGHT</div>
> </body>
> </html>
> 123456789101112131415161718192021222324252627282930313233343536373839404142
> ```
>
> 页面：
>
> ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190323161159873.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NpbmF0XzM2NDIyMjM2,size_16,color_FFFFFF,t_70)
>
> right会自动的适应宽度，这时候就形成了一个两栏自适应的布局。
>
> ###### 3.清楚浮动。
>
> 当我们不给父节点设置高度，子节点设置浮动的时候，会发生高度塌陷，这个时候我们就要清楚浮动。
>
> 比如这样：
>
> ```
> <!DOCTYPE html>
> <html lang="en">
> <head>
>     <meta charset="UTF-8">
>     <meta name="viewport" content="width=device-width, initial-scale=1.0">
>     <meta http-equiv="X-UA-Compatible" content="ie=edge">
>     <title>清除浮动</title>
> </head>
> <style>
>     .par {
>         border: 5px solid rgb(91, 243, 30);
>         width: 300px;
>     }
>     
>     .child {
>         border: 5px solid rgb(233, 250, 84);
>         width:100px;
>         height: 100px;
>         float: left;
>     }
> </style>
> <body>
>     <div class="par">
>         <div class="child"></div>
>         <div class="child"></div>
>     </div>
> </body>
> </html>
> 12345678910111213141516171819202122232425262728
> ```
>
> 页面：
>
> ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190323161720931.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NpbmF0XzM2NDIyMjM2,size_16,color_FFFFFF,t_70)
>
> 这个时候我们根据最后一条：
>
> - 计算BFC的高度时，浮动元素也参与计算。
>
> 给父节点激活BFC
>
> ```
> <!DOCTYPE html>
> <html lang="en">
> <head>
>     <meta charset="UTF-8">
>     <meta name="viewport" content="width=device-width, initial-scale=1.0">
>     <meta http-equiv="X-UA-Compatible" content="ie=edge">
>     <title>清除浮动</title>
> </head>
> <style>
>     .par {
>         border: 5px solid rgb(91, 243, 30);
>         width: 300px;
>         overflow: hidden;
>     }
>     
>     .child {
>         border: 5px solid rgb(233, 250, 84);
>         width:100px;
>         height: 100px;
>         float: left;
>     }
> </style>
> <body>
>     <div class="par">
>         <div class="child"></div>
>         <div class="child"></div>
>     </div>
> </body>
> </html>
> 1234567891011121314151617181920212223242526272829
> ```
>
> 页面：
>
> ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190323161945489.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NpbmF0XzM2NDIyMjM2,size_16,color_FFFFFF,t_70)
>
> ### 总结
>
> 以上例子都体现了：
>
> > BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。
>
> 因为BFC内部的元素和外部的元素绝对不会互相影响，因此， 当BFC外部存在浮动时，它不应该影响BFC内部Box的布局，BFC会通过变窄，而不与浮动有重叠。同样的，当BFC内部有浮动时，为了不影响外部元素的布局，BFC计算高度时会包括浮动的高度。避免margin重叠也是这样的一个道理。
>
> 摘自: https://blog.csdn.net/sinat_36422236/article/details/88763187



### [localstorage sessionstorage和cookie的区别](https://www.cnblogs.com/candy-xia/p/11561542.html)

> ## 基本概念
>
> cookie：是网景公司的前雇员在1993年发明。它的主要用于保存登陆信息，比如登陆某个网站市场可以看到'记住密码’，这就是通过在cookie中存入一段辨别用户身份的数据来实现的。
>
> sessionStorage：会话，是可以将一部分数据在当前会话中保存下来，刷新页面数据依旧存在。但是页面关闭后，sessionStorage中的数据就会被清空。
>
> localStorage：是HTML5标准中新加入的技术，当然早在IE6时代就有一个userData的东西用于本地存储，而当时考虑到浏览器的兼容性，更通用的方案是使用flash。如今localStorage被大多数浏览器所支持。
>
>  
>
> ## 三者区别
>
> **1）存储大小**
>
> cookie：一般不超过4K（因为每次http请求都会携带cookie、所以cookie只适合保存很小的数据，如会话标识）
>
> sessionStorage：5M或者更大
>
> localStorage：5M或者更大
>
> **2）数据有效期**
>
> cookie：一般由服务器生成，可以设置失效时间；若没有设置时间，关闭浏览器cookie失效，若设置了时间，cookie就会存放在硬盘里，过期才失效
>
> sessionStorage：仅在当前浏览器窗口关闭之前有效，关闭页面或者浏览器会被清除
>
> localStorage：永久有效，窗口或者浏览器关闭也会一直保存，除非手动永久清除，因此用作持久数据
>
> **3）作用域**
>
> cookie：在所有同源窗口中都是共享的
>
> sessionStorage：在同一个浏览器窗口是共享的（不同浏览器、同一个页面也是不共享的）
>
> localStorage：在所有同源窗口中都是共享的
>
> **4）通信**
>
> ccokie：十种携带在同源的http请求中，即使不需要，故cookie在浏览器和服务器之间来回传递；如果使用cookie保存过多数据会造成性能问题
>
> sessionStorage：仅在客户端（即浏览器）中保存，不参与和服务器的通信；不会自动把数据发送给服务器，仅在本地保存
>
> localStorage：仅在客户端（即浏览器）中保存，不参与和服务器的通信；不会自动把数据发送给服务器，仅在本地保存
>
> **5）易用性**
>
> cookie：需要自己进行封装，原生的cookie接口不够友好
>
> sessionStorage：原生接口可以接受，可以封装来对Object和Array有更好的支持
>
> localStorage：原生接口可以接受，可以封装来对Object和Array有更好的支持
>
>  
>
> ## 应用场景
>
> cookie：判断用户是否登录过网站，以便实现下次自动登录或记住密码；保存事件信息等
>
> sessionStorage：敏感账号一次性登录；单页面用的较多（sessionStorage 可以保证打开页面时 sessionStorage 的数据为空）
>
> localStorage：常用于长期登录（判断用户是否已登录），适合长期保存在本地的数据



### calc, support, media各自的含义及用法？

`@support`主要是用于检测浏览器是否支持CSS的某个属性，其实就是条件判断，如果支持某个属性，你可以写一套样式，如果不支持某个属性，你也可以提供另外一套样式作为替补。

calc() 函数用于动态计算长度值。 calc()函数支持 "+", "-", "*", "/" 运算；

@media 查询，你可以针对不同的媒体类型定义不同的样式。



### 手写 clear-fix

```html
 <style>
    .left{
      float: left;
    }
    .bfc{
      overflow: hidden;
    }
    /* 手写 clearfix */
    .clearfix::after{
      content: '';
      display: block;
      clear: both;
    }
  </style>
</head>
<body>
  <div class="container bfc">
    <img src="" alt="" class="left"/>
    <p class="bfc">一段文字</p>
  </div>
</body>
```

### flex 布局

常用语法加顾

1. flex-direction
2. flex-wrap
3. justify-content
4. align-self
5. align-items

能用 flex 布局, 就不要使用 float 布局 ( float 的原意是用来解决文字环绕的问题)

```html
<!-- 画骰子 -->
<style>
    .box{
      width: 200px;
      height: 200px;
      border: 2px solid #ccc;
      border-radius: 10px;
      display: flex;
      justify-content: space-between;
    }
    .item{
      display: block;
      width: 40px;
      height: 40px;
      border-radius: 50%;
      background-color: #666;
    }
    .item:nth-child(2){
      align-self: center;
    }
    .item:nth-child(3){
      align-self: flex-end;
    }
  </style>
</head>
<body>
  <div class="box">
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
  </div>  
</body>
```

### 定位问题

1. relative 相对于自身定位
2. absolute 相对于最近一层有定位元素的祖先元素定位(相对于 static 定位以外的第一个父元素进行定位)
3. 定位元素 relative absolute sticky fixed(永远相对于视口定位)
4. 当设置元素 position: absolute/ float 后, 元素的 display 值变为 block

### 圣杯布局和双飞翼布局( float 经典布局)



### CSS 水平、垂直居中的写法，请至少写出4种？

> 这题考查的是css的基础知识是否全面，所以平时一定要注意多积累

*水平居中*

- 行内元素 inline/inline-block: `text-align: center`
- 块级 block 元素: `margin: 0 auto`
- absolute 元素: left: 50% + margin-left : 负值 (一半元素的宽度)
- absolute 元素: left,right: 0 + margin: 0 auto
- absolute 元素: left: 50% + transform: translate(-50%, 0)
- `display: flex + justify-content: center`

*垂直居中*

- inline/inline-block设置line-height 等于height
- position: absolute + top: 50% + transform: translateY(-50%)
- position: absolute + top: 50% + margin-top: 负值(一半元素的高度)
- position: absolute + tob, bottom: 0 + margin: auto 0;
- `display:flex + align-items: center`
- 单元格: 父元素 display: table + display: table-cell + 子元素 vertical-align: middle; //?

最简单的水平垂直居中: 父元素 display: flex + 子元素 margin: auto



### CSS 继承

1. line-height 如何继承?

   ```html
   <style>
     /* 如下代码， P 标签的行高是多少？ */
     body{
       font-size: 20px;
       /* line-height 如何继承？
       1. 写具体数值，如30px 则继承该值
       2. 写比例，如 2/1.5，则继承该比例（先继承后计算）
       3. 写百分比， 如200%，则继承计算出来的值(先计算后继承) */
       line-height: 200%;
       /* line-height: 200%; p标签的行高是40px */
       /* line-height: 2; p标签的行高是32px*/
       /* line-height: 50px; p标签的行高是 50px*/
     }
     p{
       font-size: 16px;
     }
   </style>
   <body>
     <p>AAAA</p>
   </body>
   ```

   css 中会继承的属性还有 font-szie, color, line-height

### 选择器的权重

- 内联样式的权重为 1000

- ID 选择器的权重为 100

- 类选择器的权重为 10

- 元素选择器的权重为 1

  注: 权重计算永不进位

```css
    /* id选择器的个数 类选择器的个数 元素选择器的个数 */
    /* 0 1 0 */
    .b {
      color: purple;
    }
    /* 0 0 3 */
    html body div{
      color: red;
    }
    /* 1 0 0 */
    #b {
      color: orange;
    }
```



### 1rem、1em、1vh、1px各自代表的含义？

> rem

rem是全部的长度都相对于根元素<html>元素。通常做法是给html元素设置一个字体大小，然后其他元素的长度单位就为rem。

> em

- 子元素字体大小的em是相对于父元素字体大小
- 元素的width/height/padding/margin用em的话是相对于该元素的font-size

> vw/vh

全称是 Viewport Width 和 Viewport Height，视窗的宽度和高度，相当于 屏幕宽度和高度的 1%，不过，处理宽度的时候%单位更合适，处理高度的 话 vh 单位更好。

> px

px像素（Pixel）。相对长度单位。像素px是相对于显示器屏幕分辨率而言的。

一般电脑的分辨率有{1920*1024}等不同的分辨率

1920*1024 前者是屏幕宽度总共有1920个像素,后者则是高度为1024个像素

### 画一条0.5px的直线？

> 考查的是css3的transform

```text
height: 1px;
transform: scale(0.5);
```

### 说一下盒模型？

> 盒模型是css中重要的基础知识，也是必考的基础知识

盒模型的组成，由里向外content,padding,border,margin.

在IE盒子模型中，width表示content+padding+border这三个部分的宽度

在标准的盒子模型中，width指content部分的宽度

box-sizing的使用

```text
  box-sizing: content-box 是W3C盒子模型
  box-sizing: border-box 是IE盒子模型
```

box-sizing的默认属性是content-box

### 画一个三角形？

> 这属于简单的css考查，平时在用组件库的同时，也别忘了原生的css

```text
 .a{
            width: 0;
            height: 0;
            border-width: 100px;
            border-style: solid;
            border-color: transparent #0099CC transparent transparent;
            transform: rotate(90deg); /*顺时针旋转90°*/
 }

<div class="a"></div>
```

### 清除浮动的几种方式，及原理？

> 清除浮动简单，但这题要引出的是BFC，BFC也是必考的基础知识点

- `::after / <br> / clear: both`
- 创建父级 `BFC`(overflow:hidden)
- 父级设置高度

> *BFC （*块级格式化上下文*）*，是一个独立的渲染区域，让处于 `BFC` 内部的元素与外部的元素相互隔离，使内外元素的定位不会相互影响。

*触发条件:*

- 根元素
- `position: absolute/fixed`
- `display: inline-block / table`
- `float` 元素
- `ovevflow !== visible`

*规则:*

- 属于同一个 `BFC` 的两个相邻 `Box` 垂直排列
- 属于同一个 `BFC` 的两个相邻 `Box` 的 `margin` 会发生重叠
- `BFC` 的区域不会与 `float` 的元素区域重叠
- 计算 `BFC` 的高度时，浮动子元素也参与计算
- 文字层不会被浮动层覆盖，环绕于周围

### HTML

### 如何理解 html 语义化

- 让人更容易读懂(增加代码的可读性) 合适的标签做合适的事
- 让搜索引擎更容易读懂

### 块状元素和内联元素

- 块状元素 display: block/table; 有 div h1-6 table ul ol p 等
- 内联元素 display: inline/inline-block; 有 span img input button等



### 说一下<label>标签的用法

label标签主要是方便鼠标点击使用，扩大可点击的范围，增强用户操作体验

### 遍历A节点的父节点下的所有子节点

> 这题考查原生的js操作dom,属于非常简单的基础题，但长时间使用mvvm框架，可能会忘记

```text
<script>
    var b=document.getElementById("a").parentNode.children;
    console.log(b)
</script>
```

## JS

### 用js递归的方式写1到100求和？

> 递归我们经常用到，vue在实现双向绑定进行数据检验的时候用的也是递归，但要我们面试的时候手写一个递归，如果对递归的概念理解不透彻，可能还是会有一些问题。

```text
function add(num1,num2){
	var num = num1+num2;
        if(num2+1>100){
	 return num;
	}else{
	  return add(num,num2+1)
        }
 }
var sum =add(1,2);                 
```

### 页面渲染html的过程？

> 不需要死记硬背，理解整个过程即可

浏览器渲染页面的一般过程：

1.浏览器解析html源码，然后创建一个 DOM树。并行请求 css/image/js在DOM树中，每一个HTML标签都有一个对应的节点，并且每一个文本也都会有一个对应的文本节点。DOM树的根节点就是 documentElement，对应的是html标签。

2.浏览器解析CSS代码，计算出最终的样式数据。构建CSSOM树。对CSS代码中非法的语法它会直接忽略掉。解析CSS的时候会按照如下顺序来定义优先级：浏览器默认设置 < 用户设置 < 外链样式 < 内联样式 < html中的style。

3.DOM Tree + CSSOM --> 渲染树（rendering tree）。渲染树和DOM树有点像，但是是有区别的。

DOM树完全和html标签一一对应，但是渲染树会忽略掉不需要渲染的元素，比如head、display:none的元素等。而且一大段文本中的每一个行在渲染树中都是独立的一个节点。渲染树中的每一个节点都存储有对应的css属性。

4.一旦渲染树创建好了，浏览器就可以根据渲染树直接把页面绘制到屏幕上。

以上四个步骤并不是一次性顺序完成的。如果DOM或者CSSOM被修改，以上过程会被重复执行。实际上，CSS和JavaScript往往会多次修改DOM或者CSSOM。

### 说一下CORS？

CORS是一种新标准，支持同源通信，也支持跨域通信。fetch是实现CORS通信的

### 如何中断ajax请求？

一种是设置超时时间让ajax自动断开，另一种是手动停止ajax请求，其核心是调用XML对象的abort方法，ajax.abort()

### 说一下事件代理？

事件委托是指将事件绑定到目标元素的父元素上，利用冒泡机制触发该事件

```text
ulEl.addEventListener('click', function(e){
    var target = event.target || event.srcElement;
    if(!!target && target.nodeName.toUpperCase() === "LI"){
        console.log(target.innerHTML);
    }
}, false);
```

### target、currentTarget的区别？

currentTarget当前所绑定事件的元素

target当前被点击的元素

### 说一下宏任务和微任务？

1. 宏任务：当前调用栈中执行的任务称为宏任务。（主代码快，定时器等等）。
2. 微任务： 当前（此次事件循环中）宏任务执行完，在下一个宏任务开始之前需要执行的任务为微任务。（可以理解为回调事件，promise.then，proness.nextTick等等）。
3. 宏任务中的事件放在callback queue中，由事件触发线程维护；微任务的事件放在微任务队列中，由js引擎线程维护。

### 说一下继承的几种方式及优缺点？

> 说比较经典的几种继承方式并比较优缺点就可以了

1. 借用构造函数继承，使用call或apply方法，将父对象的构造函数绑定在子对象上
2. 原型继承，将子对象的prototype指向父对象的一个实例
3. 组合继承

原型链继承的缺点

- 字面量重写原型会中断关系，使用引用类型的原型，并且子类型还无法给超类型传递参数。

借用构造函数（类式继承）

- 借用构造函数虽然解决了刚才两种问题，但没有原型，则复用无从谈起。

组合式继承

- 组合式继承是比较常用的一种继承方法，其背后的思路是使用原型链实现对原型属性和方法的继承，而通过借用构造函数来实现对实例属性的继承。这样，既通过在原型上定义方法实现了函数复用，又保证每个实例都有它自己的属性。

### 说一下闭包？

闭包的实质是因为函数嵌套而形成的作用域链

闭包的定义即：函数 `A` 内部有一个函数 `B`，函数 `B` 可以访问到函数 `A` 中的变量，那么函数 `B` 就是闭包

### export和export default的区别？

使用上的不同

```text
export default  xxx
import xxx from './'

export xxx
import {xxx} from './'
```

### 说一下自己常用的es6的功能？

> 此题是一道开放题，可以自由回答。但要注意像let这种简单的用法就别说了，说一些经常用到并有一定高度的新功能

像module、class、promise等，尽量讲的详细一点。

### 什么是会话cookie,什么是持久cookie?

cookie是服务器返回的，指定了expire time（有效期）的是持久cookie,没有指定的是会话cookie

### 数组去重？

> 此题看着简单，但要想面试官给你高分还是有难度的。至少也要写出几种方法

js

```text
var arr=['12','32','89','12','12','78','12','32'];
    // 最简单数组去重法
    function unique1(array){
        var n = []; //一个新的临时数组
        for(var i = 0; i < array.length; i++){ //遍历当前数组
            if (n.indexOf(array[i]) == -1)
                n.push(array[i]);
        }
        return n;
    }
    arr=unique1(arr);
    // 速度最快， 占空间最多（空间换时间）
    function unique2(array){
        var n = {}, r = [], type;
        for (var i = 0; i < array.length; i++) {
            type = typeof array[i];
            if (!n[array[i]]) {
                n[array[i]] = [type];
                r.push(array[i]);
            } else if (n[array[i]].indexOf(type) < 0) {
                n[array[i]].push(type);
                r.push(array[i]);
            }
        }
        return r;
    }
    //数组下标判断法
    function unique3(array){
        var n = [array[0]]; //结果数组
        for(var i = 1; i < array.length; i++) { //从第二项开始遍历
            if (array.indexOf(array[i]) == i) 
                n.push(array[i]);
        }
        return n;
    }
```

es6

```text
es6方法数组去重
arr=[...new Set(arr)];
es6方法数组去重，第二种方法
function dedupe(array) {
  return Array.from(new Set(array));       //Array.from()能把set结构转换为数组
}
```

### get、post的区别

> 此题比较简单，但一定要回答的全面

1.get传参方式是通过地址栏URL传递，是可以直接看到get传递的参数，post传参方式参数URL不可见，get把请求的数据在URL后通过？连接，通过&进行参数分割。psot将参数存放在HTTP的包体内

2.get传递数据是通过URL进行传递，对传递的数据长度是受到URL大小的限制，URL最大长度是2048个字符。post没有长度限制

3.get后退不会有影响，post后退会重新进行提交

4.get请求可以被缓存，post不可以被缓存

5.get请求只URL编码，post支持多种编码方式

6.get请求的记录会留在历史记录中，post请求不会留在历史记录

7.get只支持ASCII字符，post没有字符类型限制

### 你所知道的http的响应码及含义？

> 此题有过开发经验的都知道几个，但还是那句话，一定要回答的详细且全面。

1xx(临时响应)

100: 请求者应当继续提出请求。

101(切换协议) 请求者已要求服务器切换协议，服务器已确认并准备进行切换。

2xx(成功)

200：正确的请求返回正确的结果

201：表示资源被正确的创建。比如说，我们 POST 用户名、密码正确创建了一个用户就可以返回 201。

202：请求是正确的，但是结果正在处理中，这时候客户端可以通过轮询等机制继续请求。

3xx(已重定向)

300：请求成功，但结果有多种选择。

301：请求成功，但是资源被永久转移。

303：使用 GET 来访问新的地址来获取资源。

304：请求的资源并没有被修改过

4xx(请求错误)

400：请求出现错误，比如请求头不对等。

401：没有提供认证信息。请求的时候没有带上 Token 等。

402：为以后需要所保留的状态码。

403：请求的资源不允许访问。就是说没有权限。

404：请求的内容不存在。

5xx(服务器错误)

500：服务器错误。

501：请求还没有被实现。



# 2020前端面试（二面面试题）

https://zhuanlan.zhihu.com/p/85030402

二面和一面不同，涉及的点比较多，主要包括：技术面、项目经理面、hr面。有些知名互联网公司会将其分为三面、四面，但考虑到大部分互联网公司最多二面，我就将部分重要内容整合在一起。

二面问题的范围比较宽广，不需要你像一面那样回答特别详细，但你一定都要有涉猎过。一般好的面试官都会按照你简历中提到过的点进行询问，所以自己简历中涉及到的知识点一定要用心准备。当然，如果面试官问不按套路出牌，问到你从来都没有涉及过的领域，切忌不懂装懂。直接说自己没有了解过，问面试官有推荐的资料学习吗即可。

说在前面，无论是答案还是见解都仅供参考，有不全或有偏颇之处，欢迎各位在评论区补充及指正。

## 项目经理

可能是项目经理也可能是技术总监，但关注的都是你的学习能力，及项目把控能力，不会像一面那样问些细碎的知识点

**最近项目中遇到什么问题，及解决方案？**

> 面试前自己一定要准备一波，不然面试的时候自己大脑中会一片空白。如果觉得自己解决的问题都没什么技术含量，那可以说项目中其他同事解决的问题，或者是自己在网上看到的问题。但前提是自己一定要搞明白，以后自己遇到了也能解决。

**最近有学习什么新技术？**

> 此题主要是想考查你平时爱不爱学习，对新技术有没有一定的敏感度。不用你有多深的领悟了解即可，但千万不能说没有。如果真的没有，就自己了解一下

**平时自己逛什么社区？**

> 主要是想了解你平时都是通过哪些途径学习，哪些娱乐社区就别说了，说一些前端方面的社区，像掘金等

**你对加班怎么看？**

> 说自己真实看法就好了，如果你说自己绝对不能加班，那就是你自己不想要这个offer

**你还有什么想要了解的吗？**

> 别问工资、五险一金啥的，这是项目经理不是hr,问一些技术团队方面的问题，这对于你以后的工作很重要

## 框架方面

只是部分的问题，希望大家能由点及面好好准备自己框架方面的知识。我建议大家准备一门框架就可以了，大体都相同，精通一门就好了。别vue、react 都是半桶水，还是要深入的去了解，我这有vue源码解析的电子书及视频，需要的可以留言。。。自己有看过，由浅入深的讲解还是挺不错的

### **单页面应用和多页面应用的优缺点？**

> 单页应用

优点：页面切换快

因为页面每次切换跳转时，并不需要做`html`文件的请求，这样就减少了`http`发送

缺点：首屏时间慢，SEO差

因为首屏时需要请求`html`，同时还要发送`js`请求，两次请求回来了，首屏才会展示出来。相对于多页应用，首屏时间慢。

SEO效果差，因为搜索引擎只认识`html`里的内容，不认识`js`的内容，而单页应用的内容都是靠`js`渲染生成出来的，搜索引擎不识别这部分内容

> 多页应用

优点：首屏时间快

因为当我们访问页面的时候，服务器返回一个html，页面就会展示出来，这个过程只经历了一个HTTP请求，所以页面展示的速度非常快。

搜索引擎优化效果好

搜索引擎在做网页排名的时候，要根据网页内容才能给网页权重，来进行网页的排名。搜索引擎是可以识别html内容的，而我们每个页面所有的内容都放在`Html`中，所以这种多页应用，seo排名效果好。

缺点：页面切换慢

因为每次跳转都需要发出一个http请求，如果网络比较慢，在页面之间来回跳转时，就会发现明显的卡顿。

### **衍生如何解决单页及多页面各自优点的问题**

### 服务端渲染

### **说一下vue<keep-alive>对应的生命周期？**

```
activated`和`deactivated
```

### **vue懒加载**

3种方式：vue异步组件、es6提案的import()、webpack的require.ensure()

### **说一下react的高阶组件？**

> 可以讲一下自己项目中实现的高阶组件，那样更具体

高阶组件是一个以组件为参数并返回一个新组件的函数，最常见的可能是 Redux 的 connect 函数。

### **说一下自己对vdom的了解？**

> 关于这个问题，大家看下我这篇文章，[前端学习，五分钟带你看懂Virtual DOM及diff算法在vue中的应用](https://zhuanlan.zhihu.com/p/82079781)，回答个80分是没有问题的

### **mvvm的双向绑定原理？**

> 理解即可，不用死记硬背

mvvm 双向绑定，采用数据劫持结合发布者-订阅者模式的方式，通过Object.defineProperty()来劫持各个属性的 setter、getter，在数据变动时发布消息给订阅者，触发相应的监听回调。

为什么要监听getter呢？因为没有getter的属性，说明页面中没有用到，就没有必要监听其setter

几个要点：

1、实现一个数据监听器 Observer，能够对数据对象的所有属性进行监听，如有变动可拿到最新值并通知订阅者

2、实现一个指令解析器 Compile，对每个元素节点的指令进行扫描和解析，根据指令模板替换数据，以及绑定相应的更新函数

3、实现一个 Watcher，作为连接 Observer 和 Compile 的桥梁，能够订阅并收到每个属性变动的通知，执行指令绑定的相应回调函数，从而更新视图

实现简单的双向绑定,大家可以阅读下这篇文章，[这应该是最详细的响应式系统讲解了](https://link.zhihu.com/?target=https%3A//juejin.im/post/5d26e368e51d4577407b1dd7)，有时间还是建议能自己敲一遍

### **vue-router的路由模式?**

hash、history

路由原理的深度剖析，大家有时间可以阅读下这篇文章，[深度剖析：前端路由原理](https://link.zhihu.com/?target=https%3A//juejin.im/post/5d469f1e5188254e1c49ae78)

### **说一下redux?**

> 理解即可，不用死记硬背。面试时详细的说一下自己的使用流程，至于细节方面，面试官还会深度的拷问

redux 是一个应用数据流框架，主要是解决了组件间状态共享的问题，主要包括三个核心方法，action，store，reducer

关于 Store：

- 整个应用只有一个唯一的 Store
- Store 对应的状态树（State），由调用一个 reducer 函数（root reducer）生成
- 状态树上的每个字段都可以进一步由不同的 reducer 函数生成
- Store 包含了几个方法比如 `dispatch`, `getState` 来处理数据流
- Store 的状态树只能由 `dispatch(action)` 来触发更改

Redux 的数据流：

- action 是一个包含 `{ type, payload }` 的对象
- reducer 函数通过 `store.dispatch(action)` 触发
- reducer 函数接受 `(state, action)` 两个参数，返回一个新的 state
- reducer 函数判断 `action.type` 然后处理对应的 `action.payload` 数据来更新状态树

所以对于整个应用来说，一个 Store 就对应一个 UI 快照，服务器端渲染就简化成了在服务器端初始化 Store，将 Store 传入应用的根组件，针对根组件调用 `renderToString` 就将整个应用输出成包含了初始化数据的 HTML。

### **说几个自己常用的vuex的api?**

store.registerModule('c',{}) //注册一个模块

store.unregisterModule('c') //解绑一个模块

store.subscribe() //订阅，每次mutations被调用，这个api都会被调用

store.subscribeAction() //监听actions

store.watch() //每次state改变之后都会调用

### **谈谈vue和react？**

这题没有对错，说出自己的见解就行，但不能空有见解，还要有理论进行支撑

> 两者的本质区别

1. vue - 本质是 MVVM 框架，由 MVC 发展而来
2. React - 本质是前端组件化框架，由后端组件化发展而来
3. vue - 使用模板（最初由 angular 提出）
4. React - 使用 JSX（jsx不是react独有的，已经成了一种标准）
5. React 本身就是组件化，没有组件化就不是 React
6. vue 也支持组件化，不过是在 MVVM 上的扩展

> 两者共同点

- 都支持组件化
- 都是数据驱动视图

> 自己的一些看法 

1. 模板语法上，我更加倾向于 JSX，因为它更接近js 语法（列如vue的循环用的是新指令v-for,而react用的是js中的map()函数）
2. 模板分离上，我更加倾向于 vue（数据和视图分离的更彻底）
3. 组件化上，我更加倾向于 React ，做的彻底
4. 国内使用，首推 vue 。文档更易读、易学、社区够大 。 如果团队水平较高，推荐使用 React 。组件化和 JSX 大型项目用react，小型项目用Vue

### **数据结构和算法**

> 至于数据结构和算法方面各个公司考查的方式完全不同，之前有给大家写过一篇[好书推荐的文章](https://zhuanlan.zhihu.com/p/82458274)，里面有一本数据结构和算法的书真的不错，有时间可以买来看看。如果时间不允许，大家只要认真准备这几点就好了

快速排序、选择排序、希尔排序、冒泡排序、波兰式和逆波兰式



## hr

大部同学都不太重视hr的面试，虽然说只要技术官和项目经理过了，一般offer就到手了，但hr是有一票否决权的，大家还是要稍微准备下，死在这就太冤了。。。

**为什么想要换工作？**

> 换工作无非于那三个原因，钱给的不够、在公司处的不开心、在公司没有上升空间。只要大家的原因积极正向一点别说公司的坏话就好了，其它自由发挥。记住千万别说公司坏话，即使前公司很操蛋

**对薪水自己有怎样的期待？**

> 自己给出一范围，别把话说太死，不同公司可以上下调整的

**对未来有一个怎样的规划？**

> 别说的太空，主要从两个方面出发，一个实近期规划，还有一个是长远规划

**你还有什么想要了解的吗？**

> 现在可以了解自己的工资、待遇、公司环境等，这里就别端着了，有什么想了解的尽管问

---

# 前端学习，五分钟带你看懂Virtual DOM及diff算法在vue中的应用

https://zhuanlan.zhihu.com/p/82079781

用过vue、React的同学一定都听过Virtual DOM（虚拟dom）及diff算法，它们给人的感觉就是深奥难懂。但大厂面试vdom(以下Virtual DOM都简称为vdom)、diff算法是绕不过去的一道坎。今天为大家揭开vdom、diff算法的神秘面纱。。

最近自己也去面试了几家公司，写了两篇前端面经，希望对大家找工作有帮助

## 什么是vdom

vdom是一种使用js对象来描述真实DOM的技术，通过这种技术,们能精确知道哪些真实DOM改变了，从而尽量减少DOM操作的性能开销。

![img](https://pic2.zhimg.com/80/v2-78c4a26fe0c5422b0fd50d0f0e42e8ad_720w.jpg)

## snabbdom.js

vdom是通过snabbdom.js库实现的,大概过程有以下三步：

1. compile（把真实DOM编译成Vnode）
2. diff（利用diff算法，比较oldVnode和newVnode之间有什么变化）
3. patch（把这些变化用打补丁的方式更新到真实dom上去）

![img](https://pic3.zhimg.com/80/v2-76dcb70180b697455f40342e59dc137e_720w.jpg)

*接下来为大家详细介绍snabbdom的两个核心函数h()、patch()*

## snabbdom - h 函数

h( ) 函数主要根据传进来的参数，返回一个 vnode（虚拟节点） 对象

![img](https://pic1.zhimg.com/80/v2-3a25ba1ae4a8f32ed4e8dfd9083c61c0_720w.jpg)

h(‘<标签名>’, {…属性…}, ‘值’)，如果值为子元素，则可以在h()函数中嵌套h(‘<标签名>’, {…属性…}, […子元素…])。

## snabbdom - patch 函数

![img](https://pic3.zhimg.com/80/v2-ce1c13134529266a9b3d1df00e11660a_720w.jpg)

patch()函数的两种使用

- **patch(container, vnode) //将虚拟dom渲染成真实的dom**

![img](https://pic2.zhimg.com/80/v2-052bcf8e67dd0fc3732e9d61a70badd9_720w.jpg)

简易的实现原理

![img](https://pic3.zhimg.com/80/v2-55bf2afb15a24e56cfc0232e94826826_720w.jpg)



- **patch(vnode, newVnode) //利用diff算法比较新旧vnode之间的差异**

简易的实现原理

![img](https://pic4.zhimg.com/80/v2-acd1e42d59ad224d0763b2a9ad9cc53f_720w.jpg)

## diff算法

> 什么是diff算法？

diff算法很早就存在了，一开始diff算法是用来计算出两个文本的差异。所以大家一定要明确，diff算法并不是react或者vue原创的，它们只是用diff算法来比较两个vnode的差异，并只针对该部分进行原生DOM操作，而非重新渲染整个页面。

*vdom中是在**patch(vnode, newVnode)**比较新旧函数时会用到diff*

以下是patch（）函数的核心代码分析

```js
function patch (oldVnode, vnode) {
    ......
    if (sameVnode(oldVnode, vnode)) {
        patchVnode(oldVnode, vnode)
    } else {
        const oEl = oldVnode.el // 当前oldVnode对应的真实元素节点
        let parentEle = api.parentNode(oEl)  // 父元素
        createEle(vnode)  // 根据Vnode生成新元素
        if (parentEle !== null) {
            api.insertBefore(parentEle, vnode.el, api.nextSibling(oEl)) // 将新元素添加进父元素
            api.removeChild(parentEle, oldVnode.el)  // 移除以前的旧元素节点
            oldVnode = null
        }
    }
    .......
    return vnode
}

patchVnode (oldVnode, vnode) {
    const el = vnode.el = oldVnode.el
    let i, oldCh = oldVnode.children, ch = vnode.children
    if (oldVnode === vnode) return
    if (oldVnode.text !== null && vnode.text !== null && oldVnode.text !== vnode.text) {
        api.setTextContent(el, vnode.text)
    }else {
        updateEle(el, vnode, oldVnode)
        if (oldCh && ch && oldCh !== ch) {
            updateChildren(el, oldCh, ch)
        }else if (ch){
            createEle(vnode) //create el's children dom
        }else if (oldCh){
            api.removeChildren(el)
        }
    }
}
```

这个函数做了以下事情：

1. 找到对应的真实dom，称为el
2. 判断Vnode和oldVnode是否完全相同，如果是，那么直接return
3. 如果他们都有文本节点并且不相等，则更新el的文本节点
4. 如果oldVnode有子节点而Vnode没有，则删除el的子节点
5. 如果oldVnode没有子节点而Vnode有，则将Vnode的子节点真实化之后添加到el
6. 如果两者都有子节点，则执行updateChildren函数比较子节点

updateChildren 函数比较复杂，感兴趣的同学可以去了解下源码。**需要vue源码解析的电子书及视频的可以留言，我发给大家**

## vue的整体流程

1. 第一步：解析模板成 render 函数
2. 第二步：响应式开始监听
3. 第三步：首次渲染，显示页面，且绑定依赖
4. 第四步：data 属性变化，触发 rerender

最近在整理vue源码学习的资料，以后会出一篇详细的vue整体流程分析文章（包含一切vue原理的面试知识点），希望能早日与各位见面

最近上新了一篇，前端开发学习过程中自己的独家好书推荐，按入门到进阶的顺序排列，无论你是出于哪个开发阶段，总有一本适合你的。

# 这应该是最详细的响应式系统讲解了

## 前言

本文从一个简单的`双向绑定`开始，逐步升级到由`defineProperty`和`Proxy`分别实现的响应式系统，注重入手思路，抓住关键细节，希望能对你有所帮助。

## 一、极简双向绑定

> 首先从最简单的双向绑定入手：

```javascript
// html
<input type="text" id="input">
<span id="span"></span>

// js
let input = document.getElementById('input')
let span = document.getElementById('span')
input.addEventListener('keyup', function(e) {
  span.innerHTML = e.target.value
})

```

以上似乎运行起来也没毛病，但我们要的是数据驱动，而不是直接操作`dom`：

```javascript
// 操作obj数据来驱动更新
let obj = {}
let input = document.getElementById('input')
let span = document.getElementById('span')
Object.defineProperty(obj, 'text', {
  configurable: true,
  enumerable: true,
  get() {
    console.log('获取数据了')
  },
  set(newVal) {
    console.log('数据更新了')
    input.value = newVal
    span.innerHTML = newVal
  }
})
input.addEventListener('keyup', function(e) {
  obj.text = e.target.value
})

```

以上就是一个简单的双向数据绑定，但显然是不足的，下面继续升级。

## 二、以defineProperty实现响应系统

在Vue3版本来临前以`defineProperty`实现的数据响应，基于发布订阅模式，其主要包含三部分：`Observer、Dep、Watcher`。

## 1. 一个思路例子

```javascript
// 需要劫持的数据
let data = {
  a: 1,
  b: {
    c: 3
  }
}

// 劫持数据data
observer(data)

// 监听订阅数据data的属性
new Watch('a', () => {
    alert(1)
})
new Watch('a', () => {
    alert(2)
})
new Watch('b.c', () => {
    alert(3)
})

```

以上就是一个简单的劫持和监听流程，那对应的`observer`和`Watch`该如何实现？

## 2. Observer

`observer`的作用就是劫持数据，将数据属性转换为访问器属性，理一下实现思路：

- ①`Observer`需要将数据转化为响应式的，那它就应该是一个函数(类)，能接收参数。
- ②为了将数据变成响应式，那需要使用`Object.defineProperty`。
- ③数据不止一种类型，这就需要递归遍历来判断。

```javascript
// 定义一个类供传入监听数据
class Observer {
  constructor(data) {
    let keys = Object.keys(data)
    for (let i = 0; i < keys.length; i++) {
      defineReactive(data, keys[i], data[keys[i]])
    }
  }
}
// 使用Object.defineProperty
function defineReactive (data, key, val) {
  // 每次设置访问器前都先验证值是否为对象，实现递归每个属性
  observer(val)
  // 劫持数据属性
  Object.defineProperty(data, key, {
    configurable: true,
    enumerable: true,
    get () {
      return val
    },
    set (newVal) {
      if (newVal === val) {
        return
      } else {
        data[key] = newVal
        // 新值也要劫持
        observer(newVal)
      }
    }
  })
}

// 递归判断
function observer (data) {
  if (Object.prototype.toString.call(data) === '[object, Object]') {
    new Observer(data)
  } else {
    return
  }
}

// 监听obj
observer(data)

```

## 3. Watcher

根据`new Watch('a', () => {alert(1)})`我们猜测`Watch`应该是这样的：

```javascript
class Watch {
  // 第一个参数为表达式，第二个参数为回调函数
  constructor (exp, cb) {
    this.exp = exp
    this.cb = cb
  }
}

```

那`Watch`和`observer`该如何关联？想想它们之间有没有关联的点？似乎可以从`exp`下手，这是它们共有的点：

```javascript
class Watch {
  // 第一个参数为表达式，第二个参数为回调函数
  constructor (exp, cb) {
    this.exp = exp
    this.cb = cb
    data[exp]   // 想想多了这句有什么作用
  }
}

```

`data[exp]`这句话是不是表示在取某个值，如果`exp`为`a`的话，那就表示`data.a`，在这之前`data`下的属性已经被我们劫持为访问器属性了，那这就表明我们能触发对应属性的`get`函数，那这就与`observer`产生了关联，那既然如此，那在触发`get`函数的时候能不能把触发者`Watch`给收集起来呢？此时就得需要一个桥梁`Dep`来协助了。

## 4. Dep

> 思路应该是`data`下的每一个属性都有一个唯一的`Dep`对象，在`get`中收集仅针对该属性的依赖，然后在`set`方法中触发所有收集的依赖，这样就搞定了，看如下代码：

```javascript
class Dep {
  constructor () {
    // 定义一个收集对应属性依赖的容器
    this.subs = []
  }
  // 收集依赖的方法
  addSub () {
    // Dep.target是个全局变量，用于存储当前的一个watcher
    this.subs.push(Dep.target)
  }
  // set方法被触发时会通知依赖
  notify () {
    for (let i = 1; i < this.subs.length; i++) {
      this.subs[i].cb()
    }
  }
}

Dep.target = null

class Watch {
  constructor (exp, cb) {
    this.exp = exp
    this.cb = cb
    // 将Watch实例赋给全局变量Dep.target，这样get中就能拿到它了
    Dep.target = this
    data[exp]
  }
}


```

此时对应的`defineReactive`我们也要增加一些代码：

```javascript
function defineReactive (data, key, val) {
  observer()
  let dep = new Dep() // 新增：这样每个属性就能对应一个Dep实例了
  Object.defineProperty(data, key, {
    configurable: true,
    enumerable: true,
    get () {
      dep.addSub() // 新增：get触发时会触发addSub来收集当前的Dep.target，即watcher
      return val
    },
    set (newVal) {
      if (newVal === val) {
        return
      } else {
        data[key] = newVal
        observer(newVal)
        dep.notify() // 新增：通知对应的依赖
      }
    }
  })
}

```

至此`observer、Dep、Watch`三者就形成了一个整体，分工明确。但还有一些地方需要处理，比如我们直接对被劫持过的对象添加新的属性是监测不到的，修改数组的元素值也是如此。这里就顺便提一下`Vue`源码中是如何解决这个问题的：

> 对于对象：`Vue`中提供了`Vue.set`和`vm.$set`这两个方法供我们添加新的属性，其原理就是先判断该属性是否为响应式的，如果不是，则通过`defineReactive`方法将其转为响应式。

> 对于数组：直接使用下标修改值还是无效的，`Vue`只`hack`了数组中的七个方法：`pop','push','shift','unshift','splice','sort','reverse'`，使得我们用起来依旧是响应式的。其原理是：在我们调用数组的这七个方法时，`Vue`会改造这些方法，它内部同样也会执行这些方法原有的逻辑，只是增加了一些逻辑：取到所增加的值，然后将其变成响应式，然后再手动出发`dep.notify()`

## 三、以Proxy实现响应系统

`Proxy`是在目标前架设一层`"拦截"`，外界对该对象的访问，都必须先通过这层拦截，因此提供了一种机制，可以对外界的访问进行过滤和改写，我们可以这样认为，`Proxy`是`Object.defineProperty`的全方位加强版。

依旧是三大件：`Observer、Dep、Watch`，我们在之前的基础再完善这三大件。

## 1. Dep

```javascript
let uid = 0 // 新增：定义一个id
class Dep {
  constructor () {
    this.id = uid++ // 新增：给dep添加id，避免Watch重复订阅
    this.subs = []
  }
  depend() {  // 新增：源码中在触发get时是先触发depend方法再进行依赖收集的，这样能将dep传给Watch
    Dep.target.addDep(this);
  }
  addSub () {
    this.subs.push(Dep.target)
  }
  notify () {
    for (let i = 1; i < this.subs.length; i++) {
      this.subs[i].cb()
    }
  }
}

```

## 2. Watch

```javascript
class Watch {
  constructor (exp, cb) {
    this.depIds = {} // 新增：储存订阅者的id，避免重复订阅
    this.exp = exp
    this.cb = cb
    Dep.target = this
    data[exp]
    // 新增：判断是否订阅过该dep，没有则存储该id并调用dep.addSub收集当前watcher
    addDep (dep) {  
      if (!this.depIds.hasOwnProperty(dep.id)) {
        dep.addSub(this)
        this.depIds[dep.id] = dep
      }
    }
    // 新增：将订阅者放入待更新队列等待批量更新
    update () {
      pushQueue(this)
    }
    // 新增：触发真正的更新操作
    run () {
      this.cb()
    }
  }
}

```

## 3. Observer

与`Object.defineProperty`监听属性不同，`Proxy`可以监听(实际是代理)整个对象，因此就不需要遍历对象的属性依次监听了，但是如果对象的属性依然是个对象，那么`Proxy`也无法监听，所以依旧使用递归套路即可。

```javascript
function Observer (data) {
  let dep = new Dep()
  return new Proxy(data, {
    get () {
      // 如果订阅者存在，进去depend方法
      if (Dep.target) {
        dep.depend()
      }
      // Reflect.get了解一下
      return Reflect.get(data, key)
    },
    set (data, key, newVal) {
      // 如果值未变，则直接返回，不触发后续操作
      if (Reflect.get(data, key) === newVal) {
        return
      } else {
        // 设置新值的同时对新值判断是否要递归监听
        Reflect.set(target, key, observer(newVal))
        // 当值被触发更改的时候，触发Dep的通知方法
        dep.notify(key)
      }
    }
  })
}

// 递归监听
function observer (data) {
  // 如果不是对象则直接返回
  if (Object.prototype.toString.call(data) !== '[object, Object]') {
    return data
  }
  // 为对象时则递归判断属性值
  Object.keys(data).forEach(key => {
    data[key] = observer(data[key])
  })
  return Observer(data)
}

// 监听obj
Observer(data)

```

至此就基本完成了三大件了，同时其不需要`hack`也能对数组进行监听。

## 四、触发依赖收集与批量异步更新

完成了响应式系统，也顺便提一下`Vue`源码中是如何触发依赖收集与批量异步更新的。

## 1. 触发依赖收集

在`Vue`源码中的`$mount`方法调用时会间接触发了一段代码：

```javascript
vm._watcher = new Watcher(vm, () => {
  vm._update(vm._render(), hydrating)
}, noop)

```

这使得`new Watcher()`会先对其传入的参数进行求值，也就间接触发了`vm._render()`，这其实就会触发了对数据的访问，进而触发属性的`get`方法而达到依赖的收集。

## 2. 批量异步更新

> `Vue`在更新`DOM`时是异步执行的。只要侦听到数据变化，`Vue`将开启一个队列，并缓冲在同一事件循环中发生的所有数据变更。如果同一个`watcher`被多次触发，只会被推入到队列中一次。这种在缓冲时去除重复数据对于避免不必要的计算和`DOM`操作是非常重要的。然后，在下一个的事件循环`“tick”`中，`Vue`刷新队列并执行实际 (已去重的) 工作。`Vue`在内部对异步队列尝试使用原生的`Promise.then、MutationObserver`和`setImmediate`，如果执行环境不支持，则会采用`setTimeout(fn, 0)`代替。

根据以上这段官方文档，这个队列主要是`异步`和`去重`，首先我们来整理一下思路：

1. 需要有一个队列来存储一个事件循环中的数据变更，且要对它去重。
2. 将当前事件循环中的数据变更添加到队列。
3. 异步的去执行这个队列中的所有数据变更。

```javascript
// 使用Set数据结构创建一个队列，这样可自动去重
let queue = new Set()

// 在属性触发set方法时会触发watcher.update，继而执行以下方法
function pushQueue (watcher) {
  // 将数据变更添加到队列
  queue.add(watcher)
  // 下一个tick执行该数据变更,所以nextTick接受的应该是一个能执行queue队列的函数
  nextTick('一个能遍历执行queue的函数')
}

// 用Promise模拟nextTick
function nextTick('一个能遍历执行queue的函数') {
  Promise.resolve().then('一个能遍历执行queue的函数')
}

```

以上已经有个大体的思路了，那接下来完成`'一个能遍历执行queue的函数'`：

```javascript
// queue是一个数组，所以直接遍历执行即可
function flushQueue () {
  queue.forEach(watcher => {
    // 触发watcher中的run方法进行真正的更新操作
    watcher.run()
  })
  // 执行后清空队列
  queue = new Set()
}

```

还有一个问题，那就是同一个事件循环中应该只要触发一次`nextTick`即可，而不是每次添加队列时都触发：

```javascript
// 设置一个是否触发了nextTick的标识
let waiting = false
function pushQueue (watcher) {
  queue.add(watcher)
  // 在以下代码执行过一次之后下次就不会执行到了，进而保证nextTick只触发一次
  if (!waiting) {
    // 保证nextTick只触发一次
    waiting = true
    nextTick('一个能遍历执行queue的函数')
  }
}

```

完整代码如下：

```javascript
// 定义队列
let queue = new Set()

// 供传入nextTick中的执行队列的函数
function flushQueue () {
  queue.forEach(watcher => {
    watcher.run()
  })
  queue = new Set()
}

// nextTick
function nextTick(flushQueue) {
  Promise.resolve().then(flushQueue)
}

// 添加到队列并调用nextTick
let waiting = false
function pushQueue (watcher) {
  queue.add(watcher)
  if (!waiting) {
    waiting = true
    nextTick(flushQueue)
  }
}

```

## 最后

以上就是响应式的一个大概原理，当然还有很多细节没说，感兴趣的可以去撸一撸源码，如果觉得有所帮助，欢迎关注点个赞！


作者：陈煜仑
链接：https://juejin.cn/post/6844903887464300552
来源：掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

# 深度剖析：前端路由原理 history hash

## 前言

前端三大框架 `Angular`、`React`、`Vue` ，它们的路由解决方案 `angular/router`、`react-router`、`vue-router` 都是基于前端路由原理进行封装实现的，因此将前端路由原理进行了解和掌握是很有必要的，因为我们再使用的过程中也难免会遇到一些坑，一旦我们掌握了它的实现原理，那么就能在开发中对路由的使用更加游刃有余。

## 一、什么是路由？

​	路由的概念起源于服务端，在以前前后端不分离的时候，由后端来控制路由，当接收到客户端发来的   `HTTP` 请求，就会根据所请求的相应 `URL`，来找到相应的映射函数，然后执行该函数，并将函数的返回值发送给客户端。对于最简单的静态资源服务器，可以认为，所有 `URL` 的映射函数就是一个文件读取操作。对于动态资源，映射函数可能是一个数据库读取操作，也可能是进行一些数据的处理等等。然后根据这些读取的数据，在服务器端就使用相应的模板来对页面进行渲染后，再返回渲染完毕的页面。它的好处与缺点非常明显：

- 好处：安全性好，`SEO` 好；
- 缺点：加大服务器的压力，不利于用户体验，代码冗合不好维护；

​	也正是由于后端路由还存在着自己的不足，前端路由才有了自己的发展空间。对于前端路由来说，路由的映射函数通常是进行一些 `DOM` 的显示和隐藏操作。这样，当访问不同的路径的时候，会显示不同的页面组件。前端路由主要有以下两种实现方案：

- `Hash`
- `History`

当然，前端路由也存在缺陷：使用浏览器的前进，后退键时会重新发送请求，来获取数据，没有合理地利用缓存。但总的来说，现在前端路由已经是实现路由的主要方式了，前端三大框架 `Angular`、`React`、`Vue` ，它们的路由解决方案 `angular/router`、`react-router`、`vue-router` 都是基于前端路由进行开发的，因此将前端路由进行了解和 掌握是很有必要的，下面我们分别对两种常见的前端路由模式 `Hash` 和 `History` 进行讲解。

## 二、前端路由的两种实现

### 2.1、Hash 模式

#### 2.1.1、原理

早期的前端路由的实现就是基于 `location.hash` 来实现的。其实现原理也很简单，`location.hash` 的值就是 `URL` 中 # 后面的内容。比如下面这个网站，它的 `location.hash` 的值为 `'#search'`：

```
https://www.word.com#search
复制代码
```

此外，`hash` 也存在下面几个特性：

- `URL` 中 `hash` 值只是客户端的一种状态，也就是说当向服务器端发出请求时，`hash` 部分不会被发送。
- `hash` 值的改变，都会在浏览器的访问历史中增加一个记录。因此我们能通过浏览器的回退、前进按钮控制`hash` 的切换。
- 我们可以使用 `hashchange` 事件来监听 `hash` 的变化。

我们可以通过两种方式触发 `hash` 变化，一种是通过 `a` 标签，并设置 `href` 属性，当用户点击这个标签后，`URL` 就会发生改变，也就会触发 `hashchange` 事件了：

```
<a href="#search">search</a>
复制代码
```

还有一种方式就是直接使用 `JavaScript`来对 `loaction.hash` 进行赋值，从而改变 `URL`，触发 `hashchange` 事件：

```
location.hash="#search"
复制代码
```

以下实现我们采用第2种方式来实现。

#### 2.1.2、实现

我们先定义一个父类 `BaseRouter`，用于实现 `Hash` 路由和 `History` 路由的一些共有方法；

```
export class BaseRouter {
  // list 表示路由表
  constructor(list) {
    this.list = list;
  }
  // 页面渲染函数
  render(state) {
    let ele = this.list.find(ele => ele.path === state);
    ele = ele ? ele : this.list.find(ele => ele.path === '*');
    ELEMENT.innerText = ele.component;
  }
}
复制代码
```

我们简单实现了 `push` 压入功能、`go` 前进/后退功能，相关代码的注释都已经标上，简单易懂，就不在一 一介绍，参见如下：

```
export class HashRouter extends BaseRouter {
  constructor(list) {
    super(list);
    this.handler();
    // 监听 hashchange 事件
    window.addEventListener('hashchange', e => {
      this.handler();
    });
  }
  // hash 改变时，重新渲染页面
  handler() {
    this.render(this.getState());
  }
  // 获取 hash 值
  getState() {
    const hash = window.location.hash;
    return hash ? hash.slice(1) : '/';
  }
  // push 新的页面
  push(path) {
    window.location.hash = path;
  }
  // 获取 默认页 url
  getUrl(path) {
    const href = window.location.href;
    const i = href.indexOf('#');
    const base = i >= 0 ? href.slice(0, i) : href;
    return base +'#'+ path;
  }
  // 替换页面
  replace(path) {
    window.location.replace(this.getUrl(path));
  }
  // 前进 or 后退浏览历史
  go(n) {
    window.history.go(n);
  }
}
复制代码
```

#### 2.1.3、效果图

`Hash` 模式的路由实现例子的效果图如下所示：



![1.png](https://user-gold-cdn.xitu.io/2019/8/4/16c5bddbc23d703a?imageslim)



### 2.2、History 模式

#### 2.2.1、原理

前面的 `hash` 虽然也很不错，但使用时都需要加上 #，并不是很美观。因此到了 `HTML5`，又提供了 `History API` 来实现 `URL` 的变化。其中做最主要的 `API` 有以下两个：`history.pushState()` 和 `history.repalceState()`。这两个 `API`可以在不进行刷新的情况下，操作浏览器的历史纪录。唯一不同的是，前者是新增一个历史记录，后者是直接替换当前的历史记录，如下所示：

```
window.history.pushState(null, null, path);
window.history.replaceState(null, null, path);
复制代码
```

此外，`history` 存在下面几个特性：

- `pushState` 和 `repalceState` 的标题（`title`）：一般浏览器会忽略，最好传入 `null` ；
- 我们可以使用 `popstate` 事件来监听 `url` 的变化；
- `history.pushState()` 或 `history.replaceState()` 不会触发 `popstate` 事件，这时我们需要手动触发页面渲染；

#### 2.2.2、实现

我们同样简单实现了 `push` 压入功能、`go` 前进/后退功能，相关代码的注释都已经标上，简单易懂，就不在一 一介绍，参见如下：

```
export class HistoryRouter extends BaseRouter {
  constructor(list) {
    super(list);
    this.handler();
    // 监听 popstate 事件
    window.addEventListener('popstate', e => {
      console.log('触发 popstate。。。');
      this.handler();
    });
  }
  // 渲染页面
  handler() {
    this.render(this.getState());
  }
  // 获取 url 
  getState() {
    const path = window.location.pathname;
    return path ? path : '/';
  }
  // push 页面
  push(path) {
    history.pushState(null, null, path);
    this.handler();
  }
  // replace 页面
  replace(path) {
    history.replaceState(null, null, path);
    this.handler();
  }
   // 前进 or 后退浏览历史
  go(n) {
    window.history.go(n);
  }
}
复制代码
```

#### 2.2.3、效果图

`History` 模式的路由实现例子的效果图如下所示：



![1.png](https://user-gold-cdn.xitu.io/2019/8/4/16c5bddbd4bc30ef?imageslim)



### 2.3、两种路由模式的对比

| 对比点 | Hash 模式               | History 模式                     |
| ------ | ----------------------- | -------------------------------- |
| 美观性 | 带着 # 字符，较丑       | 简洁美观                         |
| 兼容性 | >= ie 8，其它主流浏览器 | >= ie 10，其它主流浏览器         |
| 实用性 | 不需要对服务端做改动    | 需要服务端对路由进行相应配合设置 |

## 三、总结

本文我们大致介绍了什么路由、前端路由的源起、以及分析了两种前端路由：`Hash` 模式和 `History` 模式的原理以及简单功能实现，文中例子的代码实现已经放到 github 上面：[github.com/fengshi123/…](https://github.com/fengshi123/router-example)  。通过本文对前端路由原理的掌握，这时你就可以基础原理基础去阅读 `vue-router` 和 `react-router` 的源码实现了。

**github地址为：**[github.com/fengshi123/…](https://github.com/fengshi123/blog) **，上面汇总了作者所有的博客文章，如果喜欢或者有所启发，请帮忙给个 star ~，对作者也是一种鼓励。**


作者：我是你的超级英雄
链接：https://juejin.cn/post/6844903906024095751
来源：掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。



# VUE

## vue基础面试题

​	**1、什么是MVVM？**
答：MVVM是是Model-View-ViewModel的缩写，Model代表数据模型，定义数据操作的业务逻辑，View代表视图层，负责将数据模型渲染到页面上，ViewModel通过双向绑定把View和Model进行同步交互，不需要手动操作DOM的一种设计思想。

**2、怎么定义vue-router的动态路由？怎么获取传过来的动态参数？**
答：在router目录下的index.js文件中，对path属性加上/:id。 使用router对象的params.id

**3、vue-router有哪几种导航钩子？**
答：三种，一种是全局导航钩子：router.beforeEach(to,from,next)，作用：跳转前进行判断拦截。第二种：组件内的钩子；第三种：单独路由独享组件

**4、vuex是什么？怎么使用？哪种功能场景使用它？**

答：vue框架中状态管理。在main.js引入store，注入。新建了一个目录store，….. export 。场景有：单页应用中，组件之间的状态。音乐播放、登录状态、加入购物车

**5、MVVM和MVC区别？和其他框架(jquery)区别？那些场景适用？**

答：MVVM和MVC都是一种设计思想，主要就是MVC中的Controller演变成ViewModel,，MVVM主要通过数据来显示视图层而不是操作节点，解决了MVC中大量的DOM操作使页面渲染性能降低，加载速度慢，影响用户体验问题。主要用于数据操作比较多的场景。

场景：数据操作比较多的场景，更加便捷

**6、Vue公司的双向数据绑定原理是什么？**

答：vue.js是采用数据劫持结合发布者 - 订阅者模式的方式，通过Object.defineProperty（）来劫持各个属性的setter，getter，在数据变动时发布消息给订阅者，触发相应的监听回调。

**7、请说下封装vue组件的过程？**

答：首先，组件可以提升整个项目的开发效率能够把页面抽象成多个相对独立的模块，解决了我们传统项目开发：效率低，难维护，复用性等问题。

然后，使用Vue.extend方法创建一个组件，然后使用Vue.component方法注册组件。子组件需要数据，可以在道具中接受定义。而子组件修改好数据后，想把数据传递给父组件。可以采用发射方法

**8、聊聊你对Vue.js的模板编译的理解？**

答：简而言之，就是先转化成AST树，再得到的渲染函数返回VNODE（Vue公司的虚拟DOM节点）

详情步骤：首先，通过编译编译器把模板编译成AST语法树（抽象语法树即源代码的抽象语法结构的树状表现形式），编译是createCompiler的返回值，createCompiler是用以创建编译器的。负责合并选项。然后，AST会经过生成（将AST语法树转化成渲染功能字符串的过程）得到渲染函数，渲染的返回值是VNode，VNode是Vue的虚拟DOM节点，里面有（标签名，子节点，文本等等）

**9、<keep-alive></keep-alive>的作用是什么，如何使用？**

答：包裹动态组件时，会缓存不活动的组件实例，主要用于保留组件状态或避免重新渲染；

使用：简单页面时

缓存： <keep-alive include=”组件名”></keep-alive>

不缓存：<keep-alive exclude=”组件名”></keep-alive>

**10、vue和react区别**

答：相同点：都鼓励组件化，都有’props’的概念，都有自己的构建工具，Reat与Vue只有框架的骨架，其他的功能如路由、状态管理等是框架分离的组件。

不同点：React：数据流单向，语法—JSX，在React中你需要使用setState()方法去更新状态。Vue：数据双向绑定，语法--HTML，state对象并不是必须的，数据由data属性在Vue对象中进行管理。适用于小型应用，但对于对于大型应用而言不太适合。

**11、v-show和v-if指令的共同点和不同点?**v-show指令是通过修改元素的displayCSS属性让其显示或者隐藏。

v-if指令是直接销毁和重建DOM达到让元素显示和隐藏的效果。

**12、$route和$router的区别**

答：$route是“路由信息对象”，包括path，params，hash，query，fullPath，matched，name等路由信息参数。而$router是“路由实例”对象包括了路由的跳转方法，钩子函数等

**13、vue中 key 值的作用**

答：当 Vue.js 用 v-for 正在更新已渲染过的元素列表时，它默认用“就地复用”策略。如果数据项的顺序被改变，Vue 将不会移动 DOM 元素来匹配数据项的顺序， 而是简单复用此处每个元素，并且确保它在特定索引下显示已被渲染过的每个元素。key的作用主要是为了高效的更新虚拟DOM



# [webpack的loader和plugin的区别](https://www.cnblogs.com/tangjiao/p/10429645.html)

##  Loader

用于对模块源码的转换，loader描述了webpack如何处理非javascript模块，并且在buld中引入这些依赖。loader可以将文件从不同的语言（如TypeScript）转换为JavaScript，或者将内联图像转换为data URL。比如说：CSS-Loader，Style-Loader等。

loader的使用很简单：

在webpack.config.js中指定loader。module.rules可以指定多个loader，对项目中的各个loader有个全局概览。

loader是运行在NodeJS中，可以用options对象进行配置。plugin可以为loader带来更多特性。loader可以进行压缩，打包，语言翻译等等。

loader从模板路径解析，npm install node_modules。也可以自定义loader，命名XXX-loader。

语言类的处理器loader：CoffeeScript，TypeScript，ESNext（Bable）,Sass,Less,Stylus。任何开发技术栈都可以使用webpack。

## Plugin

目的在于解决loader无法实现的其他事，从打包优化和压缩，到重新定义环境变量，功能强大到可以用来处理各种各样的任务。webpack提供了很多开箱即用的插件：CommonChunkPlugin主要用于提取第三方库和公共模块，避免首屏加载的bundle文件，或者按需加载的bundle文件体积过大，导致加载时间过长，是一把优化的利器。而在多页面应用中，更是能够为每个页面间的应用程序共享代码创建bundle。

webpack功能强大，难点在于它的配置文件，webpack4默认不需要配置文件，可以通过mode选项为webpack指定了一些默认的配置，mode分为：development/production，默认是production。

插件可以携带参数，所以在plugins属性传入new实例。

【Mode】可以在config文件里面配置，也可以在CLI参数中配置：webpack --mode=production（一般会选择在CLI，也就是npm scripts里面进行配置）。

在webpack4以下版本，webpack3.XX，通过plugins进行环境变量的配置。

## resolve

模块，resolver是个库，帮助webpack找到bundle需要引入的模块代码，打包时，webpack使用enhanced-resolve来解析路径。 



```javascript
 resolve: {
    extensions: ['.js', '.vue', '.json'],
    alias: {
      'vue$': 'vue/dist/vue.esm.js',
      '@': resolve('src'),
    }
  }
```



## Manifest

管理所有模块之间的交互。runtime将能够查询模块标识符，检索出背后对应的模块。

*问题1：webpack通过使用bundle计算content hash作为文件名称，文件修改，新的content hash执向新的文件，缓存无效，但是文件内容没有修改，计算的hash还是会改变，因为，runtime和manifest的注入在每次构建都会发生变化。要想解决这个文件可以了解更多的runtime和manifest。*

webpack原理：从配置文件定义的模块列表开始，处理应用程序，从入口文件开始递归构建一个依赖图，然后将所有模块打包为少量的bundle，通常只有一个，可由浏览器加载。