##说说你对闭包的理解

使用闭包主要是为了设计私有的方法和变量。闭包的优点是可以避免全局变量的污染，缺点是闭包会常驻内存，会增大内存使用量，使用不当很容易造成内存泄露。



闭包有三个特性: 

>1.函数嵌套函数
>2.函数内部可以引用外部的参数和变量
>3.参数和变量不会被垃圾回收机制回收
 
请你谈谈Cookie的弊端
-----------------
`cookie`虽然在持久保存客户端数据提供了方便，分担了服务器存储的负担，但还是有很多局限性的。
第一：每个特定的域名下最多生成20个`cookie`

    1.IE6或更低版本最多20个cookie
    2.IE7和之后的版本最后可以有50个cookie。
    3.Firefox最多50个cookie
    4.chrome和Safari没有做硬性限制

`IE`和`Opera` 会清理近期最少使用的`cookie`，`Firefox`会随机清理`cookie`。

`cookie`的最大大约为`4096`字节，为了兼容性，一般不能超过`4095`字节。

IE 提供了一种存储可以持久化用户数据，叫做`userdata`，从`IE5.0`就开始支持。每个数据最多128K，每个域名下最多1M。这个持久化数据放在缓存中，如果缓存没有清理，那么会一直存在。


###优点：极高的扩展性和可用性

    1.通过良好的编程，控制保存在cookie中的session对象的大小。
    2.通过加密和安全传输技术（SSL），减少cookie被破解的可能性。
    3.只在cookie中存放不敏感数据，即使被盗也不会有重大损失。
    4.控制cookie的生命期，使之不会永远有效。偷盗者很可能拿到一个过期的cookie。

###缺点：

    1.`Cookie`数量和长度的限制。每个domain最多只能有20条cookie，每个cookie长度不能超过4KB，否则会被截掉。
    
    2.安全性问题。如果cookie被人拦截了，那人就可以取得所有的session信息。即使加密也与事无补，因为拦截者并不需要知道cookie的意义，他只要原样转发cookie就可以达到目的了。
    
    3.有些状态不可能保存在客户端。例如，为了防止重复提交表单，我们需要在服务器端保存一个计数器。如果我们把这个计数器保存在客户端，那么它起不到任何作用。

浏览器本地存储
---------
在较高版本的浏览器中，`js`提供了`sessionStorage`和`globalStorage`。在`HTML5`中提供了`localStorage`来取代`globalStorage`。

`html5`中的`Web Storage`包括了两种存储方式：`sessionStorage`和`localStorage`。

`sessionStorage`用于本地存储一个会话（session）中的数据，这些数据只有在同一个会话中的页面才能访问并且当会话结束后数据也随之销毁。因此`sessionStorage`不是一种持久化的本地存储，仅仅是会话级别的存储。

而`localStorage`用于持久化的本地存储，除非主动删除数据，否则数据是永远不会过期的。

###web storage和cookie的区别


`Web Storage`的概念和`cookie`相似，区别是它是为了更大容量存储设计的。`Cookie`的大小是受限的，并且每次你请求一个新的页面的时候`Cookie`都会被发送过去，这样无形中浪费了带宽，另外`cookie`还需要指定作用域，不可以跨域调用。

除此之外，`Web Storage`拥有`setItem,getItem,removeItem,clear`等方法，不像`cookie`需要前端开发者自己封装`setCookie，getCookie`。

但是`cookie`也是不可以或缺的：`cookie`的作用是与服务器进行交互，作为`HTTP`规范的一部分而存在 ，而`Web Storage`仅仅是为了在本地“存储”数据而生

浏览器的支持除了`IE７`及以下不支持外，其他标准浏览器都完全支持(ie及FF需在web服务器里运行)，值得一提的是IE总是办好事，例如IE7、IE6中的`userData`其实就是`javascript`本地存储的解决方案。通过简单的代码封装可以统一到所有的浏览器都支持`web storage`。



`localStorage`和`sessionStorage`都具有相同的操作方法，例如`setItem、getItem`和`removeItem`等



###cookie 和session 的区别：
 
     1、cookie数据存放在客户的浏览器上，session数据放在服务器上。
     2、cookie不是很安全，别人可以分析存放在本地的COOKIE并进行COOKIE欺骗
        考虑到安全应当使用session。
     3、session会在一定时间内保存在服务器上。当访问增多，会比较占用你服务器的性能
         考虑到减轻服务器性能方面，应当使用COOKIE。
     4、单个cookie保存的数据不能超过4K，很多浏览器都限制一个站点最多保存20个cookie。
     5、所以个人建议：
        将登陆信息等重要信息存放为SESSION
        其他信息如果需要保留，可以放在COOKIE中

CSS 相关问题
--------

###display:none和visibility:hidden的区别？
 

    display:none  隐藏对应的元素，在文档布局中不再给它分配空间，它各边的元素会合拢，
    就当他从来不存在。
    
    visibility:hidden  隐藏对应的元素，但是在文档布局中仍保留原来的空间。

###CSS中 link 和@import 的区别是？
 

    (1) link属于HTML标签，而@import是CSS提供的; 
    (2) 页面被加载的时，link会同时被加载，而@import引用的CSS会等到页面被加载完再加载;
    (3) import只在IE5以上才能识别，而link是HTML标签，无兼容问题; 
    (4) link方式的样式的权重 高于@import的权重.
    
###position:absolute和float属性的异同  
    
    A：共同点：
    对内联元素设置`float`和`absolute`属性，可以让元素脱离文档流，并且可以设置其宽高。
    
    B：不同点：
    float仍会占据位置，position会覆盖文档流中的其他元素。

###介绍一下box-sizing属性？

`box-sizing`属性主要用来控制元素的盒模型的解析模式。默认值是`content-box`。

- `content-box`：让元素维持W3C的标准盒模型。元素的宽度/高度由border + padding + content的宽度/高度决定，设置width/height属性指的是content部分的宽/高

- `border-box`：让元素维持IE传统盒模型（IE6以下版本和IE6~7的怪异模式）。设置width/height属性指的是border + padding + content


标准浏览器下，按照W3C规范对盒模型解析，一旦修改了元素的边框或内距，就会影响元素的盒子尺寸，就不得不重新计算元素的盒子尺寸，从而影响整个页面的布局。    


###CSS 选择符有哪些？哪些属性可以继承？优先级算法如何计算？ CSS3新增伪类有那些？

   
    1.id选择器（ # myid）
    2.类选择器（.myclassname）
    3.标签选择器（div, h1, p）
    4.相邻选择器（h1 + p）
    5.子选择器（ul > li）
    6.后代选择器（li a）
    7.通配符选择器（ * ）
    8.属性选择器（a[rel = "external"]）
    9.伪类选择器（a: hover, li:nth-child）
          
  *   可继承的样式： font-size font-family color, text-indent;
          
  *   不可继承的样式：border padding margin width height ;
          
  *   优先级就近原则，同权重情况下样式定义最近者为准;
          
  *   载入样式以最后载入的定位为准;
      
>优先级为:
      
      
    !important >  id > class > tag  
      
    important 比 内联优先级高,但内联比 id 要高
    
>CSS3新增伪类举例：
       
    p:first-of-type 选择属于其父元素的首个 <p> 元素的每个 <p> 元素。
    p:last-of-type  选择属于其父元素的最后 <p> 元素的每个 <p> 元素。
    p:only-of-type  选择属于其父元素唯一的 <p> 元素的每个 <p> 元素。
    p:only-child    选择属于其父元素的唯一子元素的每个 <p> 元素。
    p:nth-child(2)  选择属于其父元素的第二个子元素的每个 <p> 元素。
    :enabled  :disabled 控制表单控件的禁用状态。
    :checked        单选框或复选框被选中。
 

###position的值， relative和absolute分别是相对于谁进行定位的？

    absolute 
            生成绝对定位的元素， 相对于最近一级的 定位不是 static 的父元素来进行定位。

    fixed （老IE不支持）
        生成绝对定位的元素，相对于浏览器窗口进行定位。 

    relative 
        生成相对定位的元素，相对于其在普通流中的位置进行定位。 

    static  默认值。没有定位，元素出现在正常的流中

###CSS3有哪些新特性？

    CSS3实现圆角（border-radius），阴影（box-shadow），
    对文字加特效（text-shadow、），线性渐变（gradient），旋转（transform）
    transform:rotate(9deg) scale(0.85,0.90) translate(0px,-30px) skew(-9deg,0deg);//旋转,缩放,定位,倾斜
    增加了更多的CSS选择器  多背景 rgba 
    在CSS3中唯一引入的伪元素是::selection.
    媒体查询，多栏布局
    border-image
      
###XML和JSON的区别？


    (1).数据体积方面。
    JSON相对于XML来讲，数据的体积小，传递的速度更快些。
    (2).数据交互方面。
    JSON与JavaScript的交互更加方便，更容易解析处理，更好的数据交互。
    (3).数据描述方面。
    JSON对数据的描述性比XML较差。
    (4).传输速度方面。
    JSON的速度要远远快于XML。



###对BFC规范的理解？
          BFC，块级格式化上下文，一个创建了新的BFC的盒子是独立布局的，盒子里面的子元素的样式不会影响到外面的元素。在同一个BFC中的两个毗邻的块级盒在垂直方向（和布局方向有关系）的margin会发生折叠。
        （W3C CSS 2.1 规范中的一个概念，它决定了元素如何对其内容进行布局，以及与其他元素的关系和相互作用。）

###解释下 CSS sprites，以及你要如何在页面或网站中使用它。

    CSS Sprites其实就是把网页中一些背景图片整合到一张图片文件中，再利用CSS的“background-image”，“background- repeat”，“background-position”的组合进行背景定位，background-position可以用数字能精确的定位出背景图片的位置。这样可以减少很多图片请求的开销，因为请求耗时比较长；请求虽然可以并发，但是也有限制，一般浏览器都是6个。对于未来而言，就不需要这样做了，因为有了`http2`。



html部分
------

###说说你对语义化的理解？

    1，去掉或者丢失样式的时候能够让页面呈现出清晰的结构
    2，有利于SEO：和搜索引擎建立良好沟通，有助于爬虫抓取更多的有效信息：爬虫依赖于标签来确定上下文和各个关键字的权重；
    3，方便其他设备解析（如屏幕阅读器、盲人阅读器、移动设备）以意义的方式来渲染网页；
    4，便于团队开发和维护，语义化更具可读性，是下一步吧网页的重要动向，遵循W3C标准的团队都遵循这个标准，可以减少差异化。
    
###Doctype作用? 严格模式与混杂模式如何区分？它们有何意义?    

    （1）、<!DOCTYPE> 声明位于文档中的最前面，处于 <html> 标签之前。告知浏览器以何种模式来渲染文档。 
    
    （2）、严格模式的排版和 JS 运作模式是  以该浏览器支持的最高标准运行。
    
    （3）、在混杂模式中，页面以宽松的向后兼容的方式显示。模拟老式浏览器的行为以防止站点无法工作。
    
    （4）、DOCTYPE不存在或格式不正确会导致文档以混杂模式呈现。   

###你知道多少种Doctype文档类型？

     该标签可声明三种 DTD 类型，分别表示严格版本、过渡版本以及基于框架的 HTML 文档。
     HTML 4.01 规定了三种文档类型：Strict、Transitional 以及 Frameset。
     XHTML 1.0 规定了三种 XML 文档类型：Strict、Transitional 以及 Frameset。
    Standards （标准）模式（也就是严格呈现模式）用于呈现遵循最新标准的网页，而 Quirks
     （包容）模式（也就是松散呈现模式或者兼容模式）用于呈现为传统浏览器而设计的网页。

HTML与XHTML——二者有什么区别
-------------------

    区别：
    1.所有的标记都必须要有一个相应的结束标记
    2.所有标签的元素和属性的名字都必须使用小写
    3.所有的XML标记都必须合理嵌套
    4.所有的属性必须用引号""括起来
    5.把所有<和&特殊符号用编码表示
    6.给所有属性赋一个值
    7.不要在注释内容中使“--”
    8.图片必须有说明文字


常见兼容性问题？
--------

    * png24位的图片在iE6浏览器上出现背景，解决方案是做成PNG8.也可以引用一段脚本处理.
    
    * 浏览器默认的margin和padding不同。解决方案是加一个全局的*{margin:0;padding:0;}来统一。
    
    * IE6双边距bug:块属性标签float后，又有横行的margin情况下，在ie6显示margin比设置的大。 
    
    * 浮动ie产生的双倍距离（IE6双边距问题：在IE6下，如果对元素设置了浮动，同时又设置了margin-left或margin-right，margin值会加倍。）
      #box{ float:left; width:10px; margin:0 0 0 100px;} 
    
     这种情况之下IE会产生20px的距离，解决方案是在float的标签样式控制中加入 ——_display:inline;将其转化为行内属性。(_这个符号只有ie6会识别)
    
    *  渐进识别的方式，从总体中逐渐排除局部。 
    
      首先，巧妙的使用“\9”这一标记，将IE游览器从所有情况中分离出来。 
      接着，再次使用“+”将IE8和IE7、IE6分离开来，这样IE8已经独立识别。
    
      css
          .bb{
           background-color:#f1ee18;/*所有识别*/
          .background-color:#00deff\9; /*IE6、7、8识别*/
          +background-color:#a200ff;/*IE6、7识别*/
          _background-color:#1e0bd1;/*IE6识别*/ 
          } 
    
    *  IE下,可以使用获取常规属性的方法来获取自定义属性,
       也可以使用getAttribute()获取自定义属性;
       Firefox下,只能使用getAttribute()获取自定义属性. 
       解决方法:统一通过getAttribute()获取自定义属性.
    
    * IE下,event对象有x,y属性,但是没有pageX,pageY属性; 
      Firefox下,event对象有pageX,pageY属性,但是没有x,y属性.
    
    * 解决方法：（条件注释）缺点是在IE浏览器下可能会增加额外的HTTP请求数。
    
    * Chrome 中文界面下默认会将小于 12px 的文本强制按照 12px 显示, 
      可通过加入 CSS 属性 -webkit-text-size-adjust: none; 解决.
    
    * 超链接访问过后hover样式就不出现了 被点击访问过的超链接样式不在具有hover和active了解决方法是改变CSS属性的排列顺序:
    L-V-H-A :  a:link {} a:visited {} a:hover {} a:active {}
    
    * 怪异模式问题：漏写DTD声明，Firefox仍然会按照标准模式来解析网页，但在IE中会触发怪异模式。为避免怪异模式给我们带来不必要的麻烦，最好养成书写DTD声明的好习惯。现在可以使用[html5](http://www.w3.org/TR/html5/single-page.html)推荐的写法：`<doctype html>`
    
    * 上下margin重合问题
    ie和ff都存在，相邻的两个div的margin-left和margin-right不会重合，但是margin-top和margin-bottom却会发生重合。
    解决方法，养成良好的代码编写习惯，同时采用margin-top或者同时采用margin-bottom。
    * ie6对png图片格式支持不好(引用一段脚本处理)


    
###解释下浮动和它的工作原理？清除浮动的技巧

    浮动元素脱离文档流，不占据空间。浮动元素碰到包含它的边框或者浮动元素的边框停留。
    
    1.使用空标签清除浮动。
       这种方法是在所有浮动标签后面添加一个空标签 定义css clear:both. 弊端就是增加了无意义标签。
    2.使用overflow。
       给包含浮动元素的父标签添加css属性 overflow:auto; zoom:1; zoom:1用于兼容IE6。
    3.使用after伪对象清除浮动。
       该方法只适用于非IE浏览器。具体写法可参照以下示例。使用中需注意以下几点。一、该方法中必须为需要清除浮动元素的伪对象中设置 height:0，否则该元素会比实际高出若干像素；

###浮动元素引起的问题和解决办法？

    浮动元素引起的问题：

    （1）父元素的高度无法被撑开，影响与父元素同级的元素
    （2）与浮动元素同级的非浮动元素（内联元素）会跟随其后
    （3）若非第一个元素浮动，则该元素之前的元素也需要浮动，否则会影响页面显示的结构

解决方法：
使用`CSS`中的`clear:both`;属性来清除元素的浮动可解决2、3问题，对于问题1，添加如下样式，给父元素添加`clearfix`样式：

    .clearfix:after{content: ".";display: block;height: 0;clear: both;visibility: hidden;}
    .clearfix{display: inline-block;} /* for IE/Mac */

**清除浮动的几种方法：**

    1，额外标签法，<div style="clear:both;"></div>（缺点：不过这个办法会增加额外的标签使HTML结构看起来不够简洁。）
    2，使用after伪类

    #parent:after{
        content:".";
        height:0;
        visibility:hidden;
        display:block;
        clear:both;
        }
    
    3,浮动外部元素
    4,设置`overflow`为`hidden`或者auto

###IE 8以下版本的浏览器中的盒模型有什么不同

    IE8以下浏览器的盒模型中定义的元素的宽高不包括内边距和边框

###DOM操作——怎样添加、移除、移动、复制、创建和查找节点。 

    （1）创建新节点
    
          createDocumentFragment()    //创建一个DOM片段
    
          createElement()   //创建一个具体的元素
    
          createTextNode()   //创建一个文本节点
    
    （2）添加、移除、替换、插入
    
          appendChild()
    
          removeChild()
    
          replaceChild()
    
          insertBefore() //在已有的子节点前插入一个新的子节点
    
    （3）查找
    
          getElementsByTagName()    //通过标签名称
    
          getElementsByName()    //通过元素的Name属性的值(IE容错能力较强，会得到一个数组，其中包括id等于name值的)
    
          getElementById()    //通过元素Id，唯一性

###html5有哪些新特性、移除了那些元素？如何处理HTML5新标签的浏览器兼容问题？如何区分 HTML 和 HTML5？

    * HTML5 现在已经不是 SGML 的子集，主要是关于图像，位置，存储，多任务等功能的增加。
    
    * 拖拽释放(Drag and drop) API 
      语义化更好的内容标签（header,nav,footer,aside,article,section）
      音频、视频API(audio,video)
      画布(Canvas) API
      地理(Geolocation) API
      本地离线存储 localStorage 长期存储数据，浏览器关闭后数据不丢失；
      sessionStorage 的数据在浏览器关闭后自动删除
    
      表单控件，calendar、date、time、email、url、search  
      新的技术webworker, websocket, Geolocation
    
    * 移除的元素
    
    纯表现的元素：basefont，big，center，font, s，strike，tt，u；
    
    对可用性产生负面影响的元素：frame，frameset，noframes；
    
    支持HTML5新标签：
    
    * IE8/IE7/IE6支持通过document.createElement方法产生的标签，
      可以利用这一特性让这些浏览器支持HTML5新标签，
    
      浏览器支持新标签后，还需要添加标签默认的样式：
    
    * 当然最好的方式是直接使用成熟的框架、使用最多的是html5shim框架
       <!--[if lt IE 9]> 
       <script> src="http://html5shim.googlecode.com/svn/trunk/html5.js"</script> 
       <![endif]--> 
    如何区分： DOCTYPE声明\新增的结构元素\功能元素

iframe的优缺点？
------------

    1.`<iframe>`优点：
    
        解决加载缓慢的第三方内容如图标和广告等的加载问题
        Security sandbox
        并行加载脚本
    
    2.`<iframe>`的缺点：
     
    
        *iframe会阻塞主页面的Onload事件；
        
        *即时内容为空，加载也需要时间
        *没有语意 

如何实现浏览器内多个标签页之间的通信?
-------------------


    调用localstorge、cookies等本地存储方式
    

    

线程与进程的区别
--------

    一个程序至少有一个进程,一个进程至少有一个线程. 
    线程的划分尺度小于进程，使得多线程程序的并发性高。 
    另外，进程在执行过程中拥有独立的内存单元，而多个线程共享内存，从而极大地提高了程序的运行效率。 
    线程在执行过程中与进程还是有区别的。每个独立的线程有一个程序运行的入口、顺序执行序列和程序的出口。但是线程不能够独立执行，必须依存在应用程序中，由应用程序提供多个线程执行控制。 
    从逻辑角度来看，多线程的意义在于一个应用程序中，有多个执行部分可以同时执行。但操作系统并没有将多个线程看做多个独立的应用，来实现进程的调度和管理以及资源分配。这就是进程和线程的重要区别。


你如何对网站的文件和资源进行优化？
-----------------

    期待的解决方案包括：
     文件合并
     文件最小化/文件压缩
     使用 CDN 托管
     缓存的使用（多个域名来提供缓存）
     其他

请说出三种减少页面加载时间的方法。
-----------------

     1.优化图片 
     2.图像格式的选择（GIF：提供的颜色较少，可用在一些对颜色要求不高的地方） 
     3.优化CSS（压缩合并css，如margin-top,margin-left...) 
     4.网址后加斜杠（如www.campr.com/目录，会判断这个“目录是什么文件类型，或者是目录。） 
     5.标明高度和宽度（如果浏览器没有找到这两个参数，它需要一边下载图片一边计算大小，如果图片很多，浏览器需要不断地调整页面。这不但影响速度，也影响浏览体验。 
    当浏览器知道了高度和宽度参数后，即使图片暂时无法显示，页面上也会腾出图片的空位，然后继续加载后面的内容。从而加载时间快了，浏览体验也更好了。） 
    
    6.减少http请求（合并文件，合并图片）。


你都使用哪些工具来测试代码的性能？
-----------------

    Profiler, JSPerf（http://jsperf.com/nexttick-vs-setzerotimeout-vs-settimeout）, Dromaeo


什么是 FOUC（无样式内容闪烁）？你如何来避免 FOUC？
------------------------------

     FOUC - Flash Of Unstyled Content 文档样式闪烁
     <style type="text/css" media="all">@import "../fouc.css";</style> 
    而引用CSS文件的@import就是造成这个问题的罪魁祸首。IE会先加载整个HTML文档的DOM，然后再去导入外部的CSS文件，因此，在页面DOM加载完成到CSS导入完成中间会有一段时间页面上的内容是没有样式的，这段时间的长短跟网速，电脑速度都有关系。
     解决方法简单的出奇，只要在<head>之间加入一个<link>或者<script>元素就可以了。

null和undefined的区别？
------------------

`null`是一个表示"无"的对象，转为数值时为0；`undefined`是一个表示"无"的原始值，转为数值时为`NaN`。  
  
当声明的变量还未被初始化时，变量的默认值为`undefined`。
`null`用来表示尚未存在的对象，常用来表示函数企图返回一个不存在的对象。 

`undefined`表示"缺少值"，就是此处应该有一个值，但是还没有定义。典型用法是：

    （1）变量被声明了，但没有赋值时，就等于undefined。

    （2) 调用函数时，应该提供的参数没有提供，该参数等于undefined。

    （3）对象没有赋值的属性，该属性的值为undefined。

    （4）函数没有返回值时，默认返回undefined。

`null`表示"没有对象"，即该处不应该有值。典型用法是：

    （1） 作为函数的参数，表示该函数的参数不是对象。

    （2） 作为对象原型链的终点。



new操作符具体干了什么呢?
--------------

       1、创建一个空对象，并且 this 变量引用该对象，同时还继承了该函数的原型。
       2、属性和方法被加入到 this 引用的对象中。
       3、新创建的对象由 this 所引用，并且最后隐式的返回 this 。
    
    var obj  = {};
    obj.__proto__ = Base.prototype;
    Base.call(obj); 



js延迟加载的方式有哪些？
-------------

    defer和async、动态创建DOM方式（创建script，插入到DOM中，加载完毕后callBack）、按需异步载入js

如何解决跨域问题?
---------

        jsonp、 document.domain+iframe、window.name、window.postMessage、服务器上设置代理页面
        
    jsonp的原理是动态插入script标签
    
    
具体参见：[详解js跨域问题][2]


documen.write和 innerHTML的区别
---------------------------

    document.write只能重绘整个页面
    
    innerHTML可以重绘页面的一部分

.call() 和 .apply() 的区别和作用？
-----------------------
作用：动态改变某个类的某个方法的运行环境。
区别参见：[JavaScript学习总结（四）function函数部分][3]

哪些操作会造成内存泄漏？
------------

    内存泄漏指任何对象在您不再拥有或需要它之后仍然存在。
    垃圾回收器定期扫描对象，并计算引用了每个对象的其他对象的数量。如果一个对象的引用数量为 0（没有其他对象引用过该对象），或对该对象的惟一引用是循环的，那么该对象的内存即可回收。
    
    setTimeout 的第一个参数使用字符串而非函数的话，会引发内存泄漏。
    闭包、控制台日志、循环（在两个对象彼此引用且彼此保留时，就会产生一个循环）

详见：[详解js变量、作用域及内存][4]

JavaScript中的作用域与变量声明提升？
-----------------------

详见：[详解JavaScript函数模式][5]

如何判断当前脚本运行在浏览器还是node环境中？
------------------------

    通过判断Global对象是否为window，如果不为window，当前脚本没有运行在浏览器中
    

其他问题？
-----
###你遇到过比较难的技术问题是？你是如何解决的？


###列举IE 与其他浏览器不一样的特性？



###什么叫优雅降级和渐进增强？

    优雅降级：Web站点在所有新式浏览器中都能正常工作，如果用户使用的是老式浏览器，则代码会检查以确认它们是否能正常工作。由于IE独特的盒模型布局问题，针对不同版本的IE的hack实践过优雅降级了,为那些无法支持功能的浏览器增加候选方案，使之在旧式浏览器上以某种形式降级体验却不至于完全失效.
    
    渐进增强：从被所有浏览器支持的基本功能开始，逐步地添加那些只有新式浏览器才支持的功能,向页面增加无害于基础浏览器的额外样式和功能的。当浏览器支持时，它们会自动地呈现出来并发挥作用。

详见：[css学习归纳总结（一）][6]

###WEB应用从服务器主动推送Data到客户端有那些方式？

Javascript数据推送

>Commet：基于HTTP长连接的服务器推送技术

>基于WebSocket的推送方案

>SSE（Server-Send Event）：服务器推送数据新方式




###对前端界面工程师这个职位是怎么样理解的？它的前景会怎么样？

    前端是最贴近用户的程序员，比后端、数据库、产品经理、运营、安全都近。
        1、实现界面交互
        2、提升用户体验
        3、有了Node.js，前端可以实现服务端的一些事情
    
    
    前端是最贴近用户的程序员，前端的能力就是能让产品从 90分进化到 100 分，甚至更好，
    
     参与项目，快速高质量完成实现效果图，精确到1px；
    
     与团队成员，UI设计，产品经理的沟通；
    
     做好的页面结构，页面重构和用户体验；
    
     处理hack，兼容、写出优美的代码格式；
    
     针对服务器的优化、拥抱最新前端技术。



你有哪些性能优化的方法？
------------

 （[详情请看雅虎14条性能优化原则][7]）。
    
      （1） 减少http请求次数：CSS Sprites, JS、CSS源码压缩、图片大小控制合适；网页Gzip，CDN托管，data缓存 ，图片服务器。
    
      （2） 前端模板 JS+数据，减少由于HTML标签导致的带宽浪费，前端用变量保存AJAX请求结果，每次操作本地变量，不用请求，减少请求次数
    
      （3） 用innerHTML代替DOM操作，减少DOM操作次数，优化javascript性能。
    
      （4） 当需要设置的样式很多时设置className而不是直接操作style。
    
      （5） 少用全局变量、缓存DOM节点查找的结果。减少IO读取操作。
    
      （6） 避免使用CSS Expression（css表达式)又称Dynamic properties(动态属性)。
    
      （7） 图片预加载，将样式表放在顶部，将脚本放在底部  加上时间戳。



详情：http://segmentfault.com/blog/trigkit4/1190000000691919

一个页面从输入 URL 到页面加载显示完成，这个过程中都发生了什么？
----------------------------------

     

        分为4个步骤：
        （1），当发送一个URL请求时，不管这个URL是Web页面的URL还是Web页面上每个资源的URL，浏览器都会开启一个线程来处理这个请求，同时在远程DNS服务器上启动一个DNS查询。这能使浏览器获得请求对应的IP地址。
        （2）， 浏览器与远程Web服务器通过TCP三次握手协商来建立一个TCP/IP连接。该握手包括一个同步报文，一个同步-应答报文和一个应答报文，这三个报文在 浏览器和服务器之间传递。该握手首先由客户端尝试建立起通信，而后服务器应答并接受客户端的请求，最后由客户端发出该请求已经被接受的报文。
        （3），一旦TCP/IP连接建立，浏览器会通过该连接向远程服务器发送HTTP的GET请求。远程服务器找到资源并使用HTTP响应返回该资源，值为200的HTTP响应状态表示一个正确的响应。
        （4），此时，Web服务器提供资源服务，客户端开始下载资源。
        
    请求返回后，便进入了我们关注的前端模块
    简单来说，浏览器会解析HTML生成DOM Tree，其次会根据CSS生成CSS Rule Tree，而javascript又可以根据DOM API操作DOM

详情：[从输入 URL 到浏览器接收的过程中发生了什么事情？][8]

平时如何管理你的项目？
-----------

    先期团队必须确定好全局样式（globe.css），编码模式(utf-8) 等；
    
            编写习惯必须一致（例如都是采用继承式的写法，单样式都写成一行）；
    
            标注样式编写人，各模块都及时标注（标注关键样式调用的地方）；
    
            页面进行标注（例如 页面 模块 开始和结束）；
    
            CSS跟HTML 分文件夹并行存放，命名都得统一（例如style.css）；
    
            JS 分文件夹存放 命名以该JS功能为准的英文翻译。
    
            图片采用整合的 images.png png8 格式文件使用 尽量整合在一起使用方便将来的管理 
            
说说最近最流行的一些东西吧？常去哪些网站？
--------------------------

    Node.js、Mongodb、npm、MVVM、MEAN、three.js,React 。
    网站：w3cfuns,sf,hacknews,CSDN,慕课，博客园，InfoQ,w3cplus等

javascript对象的几种创建方式
-------------------

    1，工厂模式
    2，构造函数模式
    3，原型模式
    4，混合构造函数和原型模式
    5，动态原型模式
    6，寄生构造函数模式
    7，稳妥构造函数模式

javascript继承的6种方法
-----------------

    1，原型链继承
    2，借用构造函数继承
    3，组合继承(原型+借用构造)
    4，原型式继承
    5，寄生式继承
    6，寄生组合式继承

详情：[JavaScript继承方式详解][9]
ajax过程
------

    (1)创建XMLHttpRequest对象,也就是创建一个异步调用对象.
    
    (2)创建一个新的HTTP请求,并指定该HTTP请求的方法、URL及验证信息.
    
    (3)设置响应HTTP请求状态变化的函数.
    
    (4)发送HTTP请求.
    
    (5)获取异步调用返回的数据.
    
    (6)使用JavaScript和DOM实现局部刷新.

详情：[JavaScript学习总结（七）Ajax和Http状态字][10]

异步加载和延迟加载
---------

    1.异步加载的方案： 动态插入script标签
    2.通过ajax去获取js代码，然后通过eval执行
    3.script标签上添加defer或者async属性
    4.创建并插入iframe，让它异步执行js
    5.延迟加载：有些 js 代码并不是页面初始化的时候就立刻需要的，而稍后的某些情况才需要的。

前端安全问题？
-------
###sql注入原理

就是通过把`SQL`命令插入到`Web`表单递交或输入域名或页面请求的查询字符串，最终达到欺骗服务器执行恶意的SQL命令。

总的来说有以下几点：

    1.永远不要信任用户的输入，要对用户的输入进行校验，可以通过正则表达式，或限制长度，对单引号和双"-"进行转换等。
    2.永远不要使用动态拼装SQL，可以使用参数化的SQL或者直接使用存储过程进行数据查询存取。
    3.永远不要使用管理员权限的数据库连接，为每个应用使用单独的权限有限的数据库连接。
    4.不要把机密信息明文存放，请加密或者hash掉密码和敏感的信息。

###XSS原理及防范

`Xss(cross-site scripting)`攻击指的是攻击者往Web页面里插入恶意`html`标签或者`javascript`代码。比如：攻击者在论坛中放一个
看似安全的链接，骗取用户点击后，窃取cookie中的用户私密信息；或者攻击者在论坛中加一个恶意表单，
当用户提交表单的时候，却把信息传送到攻击者的服务器中，而不是用户原本以为的信任站点。

###XSS防范方法

1.代码里对用户输入的地方和变量都需要仔细检查长度和对`”<”,”>”,”;”,”’”`等字符做过滤；其次任何内容写到页面之前都必须加以`encode`，避免不小心把`html tag` 弄出来。这一个层面做好，至少可以堵住超过一半的`XSS` 攻击。
<br/>
2.避免直接在`cookie` 中泄露用户隐私，例如`email`、密码等等。
3.通过使cookie 和系统ip 绑定来降低`cookie` 泄露后的危险。这样攻击者得到的cookie 没有实际价值，不可能拿来重放。
<br/>
4.尽量采用POST 而非GET 提交表单

###XSS与CSRF有什么区别吗？

`XSS`是获取信息，不需要提前知道其他用户页面的代码和数据包。`CSRF`是代替用户完成指定的动作，需要知道其他用户页面的代码和数据包。

要完成一次CSRF攻击，受害者必须依次完成两个步骤：

　　1.登录受信任网站A，并在本地生成Cookie。
　　2.在不登出A的情况下，访问危险网站B。

###CSRF的防御

1.服务端的CSRF方式方法很多样，但总的思想都是一致的，就是在客户端页面增加伪随机数。
2.使用验证码

ie各版本和chrome可以并行下载多少个资源
-----------------------

    IE6 两个并发，iE7升级之后的6个并发，之后版本也是6个
    
    Firefox，chrome也是6个

javascript里面的继承怎么实现，如何避免原型链上面的对象共享
----------------------------------

    用构造函数和原型链的混合模式去实现继承，避免对象共享可以参考经典的extend()函数，很多前端框架都有封装的，就是用一个空函数当做中间变量


grunt， YUI compressor 和 google clojure用来进行代码压缩的用法。
--------------------------------------------------

    YUI Compressor 是一个用来压缩 JS 和 CSS 文件的工具，采用Java开发。
    
    使用方法：
    
    //压缩JS
    java -jar yuicompressor-2.4.2.jar --type js --charset utf-8 -v src.js > packed.js
    //压缩CSS
    java -jar yuicompressor-2.4.2.jar --type css --charset utf-8 -v src.css > packed.css

详情请见：[你需要掌握的前端代码性能优化工具][11] 

Flash、Ajax各自的优缺点，在使用中如何取舍？
--------------------------

    1、Flash ajax对比
    Flash适合处理多媒体、矢量图形、访问机器；对CSS、处理文本上不足，不容易被搜索。
    Ajax对CSS、文本支持很好，支持搜索；多媒体、矢量图形、机器访问不足。
    共同点：与服务器的无刷新传递消息、用户离线和在线状态、操作DOM


请解释一下 JavaScript 的同源策略。
-----------------------
概念:同源策略是客户端脚本（尤其是`Javascript`）的重要的安全度量标准。它最早出自`Netscape Navigator2.0`，其目的是防止某个文档或脚本从多个不同源装载。

这里的同源策略指的是：协议，域名，端口相同，同源策略是一种安全协议。
指一段脚本只能读取来自同一来源的窗口和文档的属性。

###为什么要有同源限制？
   我们举例说明：比如一个黑客程序，他利用`Iframe`把真正的银行登录页面嵌到他的页面上，当你使用真实的用户名，密码登录时，他的页面就可以通过`Javascript`读取到你的表单中`input`中的内容，这样用户名，密码就轻松到手了。



什么是 "use strict"; ? 使用它的好处和坏处分别是什么？
-----------------------------------
`ECMAscript 5`添加了第二种运行模式："严格模式"（strict mode）。顾名思义，这种模式使得`Javascript`在更严格的条件下运行。


设立"严格模式"的目的，主要有以下几个：



    - 消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为;
    - 消除代码运行的一些不安全之处，保证代码运行的安全；
    - 提高编译器效率，增加运行速度；
    - 为未来新版本的Javascript做好铺垫。

注：经过测试`IE6,7,8,9`均不支持严格模式。

缺点：
现在网站的`JS` 都会进行压缩，一些文件用了严格模式，而另一些没有。这时这些本来是严格模式的文件，被 `merge` 后，这个串就到了文件的中间，不仅没有指示严格模式，反而在压缩后浪费了字节。

GET和POST的区别，何时使用POST？
-----------

        GET：一般用于信息获取，使用URL传递参数，对所发送信息的数量也有限制，一般在2000个字符
        POST：一般用于修改服务器上的资源，对所发送的信息没有限制。
        
        GET方式需要使用Request.QueryString来取得变量的值，而POST方式通过Request.Form来获取变量的值，
        也就是说Get是通过地址栏来传值，而Post是通过提交表单来传值。
    
    然而，在以下情况中，请使用 POST 请求：
    无法使用缓存文件（更新服务器上的文件或数据库）
    向服务器发送大量数据（POST 没有数据量限制）
    发送包含未知字符的用户输入时，POST 比 GET 更稳定也更可靠

哪些地方会出现css阻塞，哪些地方会出现js阻塞？
-----------------------------------

**js的阻塞特性：**所有浏览器在下载`JS`的时候，会阻止一切其他活动，比如其他资源的下载，内容的呈现等等。直到`JS`下载、解析、执行完毕后才开始继续`并行下载`其他资源并呈现内容。为了提高用户体验，新一代浏览器都支持并行下载`JS`，但是`JS`下载仍然会阻塞其它资源的下载（例如.图片，css文件等）。

由于浏览器为了防止出现`JS`修改`DOM`树，需要重新构建`DOM`树的情况，所以就会阻塞其他的下载和呈现。

嵌入`JS`会阻塞所有内容的呈现，而外部`JS`只会阻塞其后内容的显示，2种方式都会阻塞其后资源的下载。也就是说外部样式不会阻塞外部脚本的加载，但会阻塞外部脚本的执行。

`CSS`怎么会阻塞加载了？`CSS`本来是可以并行下载的，在什么情况下会出现阻塞加载了(在测试观察中，`IE6`下`CSS`都是阻塞加载）

当`CSS`后面跟着嵌入的`JS`的时候，该`CSS`就会出现阻塞后面资源下载的情况。而当把嵌入`JS`放到`CSS`前面，就不会出现阻塞的情况了。



 根本原因：因为浏览器会维持`html`中`css`和`js`的顺序，样式表必须在嵌入的JS执行前先加载、解析完。而嵌入的`JS`会阻塞后面的资源加载，所以就会出现上面`CSS`阻塞下载的情况。

嵌入`JS`应该放在什么位置？

       1、放在底部，虽然放在底部照样会阻塞所有呈现，但不会阻塞资源下载。
       
       2、如果嵌入JS放在head中，请把嵌入JS放在CSS头部。
       
       3、使用defer（只支持IE）
       
       4、不要在嵌入的JS中调用运行时间较长的函数，如果一定要用，可以用`setTimeout`来调用

###Javascript无阻塞加载具体方式

 - **将脚本放在底部。**`<link>`还是放在`head`中，用以保证在`js`加载前，能加载出正常显示的页面。`<script>`标签放在`</body>`前。
 - **成组脚本**：由于每个`<script>`标签下载时阻塞页面解析过程，所以限制页面的`<script>`总数也可以改善性能。适用于内联脚本和外部脚本。

 

 - **非阻塞脚本**：等页面完成加载后，再加载`js`代码。也就是，在`window.onload`事件发出后开始下载代码。
    （1）`defer`属性：支持IE4和`fierfox3.5`更高版本浏览器
    （2）动态脚本元素：文档对象模型（DOM）允许你使用js动态创建`HTML`的几乎全部文档内容。代码如下：
    
<br>

    <script>
    var script=document.createElement("script");
    script.type="text/javascript";
    script.src="file.js";
    document.getElementsByTagName("head")[0].appendChild(script);
    </script>

 此技术的重点在于：无论在何处启动下载，文件额下载和运行都不会阻塞其他页面处理过程。即使在head里（除了用于下载文件的http链接）。   
    

闭包相关问题？
-------
详情请见：[详解js闭包][12]
    

js事件处理程序问题？
-----------
详情请见：[JavaScript学习总结（九）事件详解][13]
    
    

eval是做什么的？
----------

    它的功能是把对应的字符串解析成JS代码并运行；
    应该避免使用eval，不安全，非常耗性能（2次，一次解析成js语句，一次执行）。

    

JavaScript原型，原型链 ? 有什么特点？
-------------------------

    *  原型对象也是普通的对象，是对象一个自带隐式的 __proto__ 属性，原型也有可能有自己的原型，如果一个原型对象的原型不为null的话，我们就称之为原型链。
    *  原型链是由一些用来继承和共享属性的对象组成的（有限的）对象链。




事件、IE与火狐的事件机制有什么区别？ 如何阻止冒泡？
---------------------------


     1. 我们在网页中的某个操作（有的操作对应多个事件）。例如：当我们点击一个按钮就会产生一个事件。是可以被 JavaScript 侦测到的行为。  
     2. 事件处理机制：IE是事件冒泡、firefox同时支持两种事件模型，也就是：捕获型事件和冒泡型事件。；
     3.  ev.stopPropagation();注意旧ie的方法 ev.cancelBubble = true;

ajax 是什么?ajax 的交互模型?同步和异步的区别?如何解决跨域问题?
--------------------------------------
详情请见：[JavaScript学习总结（七）Ajax和Http状态字][14]
    

  

    1. 通过异步模式，提升了用户体验
    
      2. 优化了浏览器和服务器之间的传输，减少不必要的数据往返，减少了带宽占用
    
      3. Ajax在客户端运行，承担了一部分本来由服务器承担的工作，减少了大用户量下的服务器负载。
    
      2. Ajax的最大的特点是什么。
    
      Ajax可以实现动态不刷新（局部刷新）
      readyState属性 状态 有5个可取值： 0=未初始化 ，1=启动 2=发送，3=接收，4=完成
    
    ajax的缺点
    
      1、ajax不支持浏览器back按钮。
    
      2、安全问题 AJAX暴露了与服务器交互的细节。
    
      3、对搜索引擎的支持比较弱。
    
      4、破坏了程序的异常机制。
    
      5、不容易调试。
    
    跨域： jsonp、 iframe、window.name、window.postMessage、服务器上设置代理页面

js对象的深度克隆
---------


      function clone(Obj) {   
            var buf;   
            if (Obj instanceof Array) {   
                buf = [];  //创建一个空的数组 
                var i = Obj.length;   
                while (i--) {   
                    buf[i] = clone(Obj[i]);   
                }   
                return buf;   
            }else if (Obj instanceof Object){   
                buf = {};  //创建一个空对象 
                for (var k in Obj) {  //为这个对象添加新的属性 
                    buf[k] = clone(Obj[k]);   
                }   
                return buf;   
            }else{   
                return Obj;   
            }   
        }  
    

AMD和CMD 规范的区别？
--------------
详情请见：[详解JavaScript模块化开发][15] 

网站重构的理解？
--------

    网站重构：在不改变外部行为的前提下，简化结构、添加可读性，而在网站前端保持一致的行为。也就是说是在不改变UI的情况下，对网站进行优化，在扩展的同时保持一致的UI。
    
    对于传统的网站来说重构通常是：
    
    表格(table)布局改为DIV+CSS
    使网站前端兼容于现代浏览器(针对于不合规范的CSS、如对IE6有效的)
    对于移动平台的优化
    针对于SEO进行优化
    深层次的网站重构应该考虑的方面
    
    减少代码间的耦合
    让代码保持弹性
    严格按规范编写代码
    设计可扩展的API
    代替旧有的框架、语言(如VB)
    增强用户体验
    通常来说对于速度的优化也包含在重构中
    
    压缩JS、CSS、image等前端资源(通常是由服务器来解决)
    程序的性能优化(如数据读写)
    采用CDN来加速资源加载
    对于JS DOM的优化
    HTTP服务器的文件缓存

如何获取UA？
-------

    <script> 
        function whatBrowser() {  
            document.Browser.Name.value=navigator.appName;  
            document.Browser.Version.value=navigator.appVersion;  
            document.Browser.Code.value=navigator.appCodeName;  
            document.Browser.Agent.value=navigator.userAgent;  
        }  
    </script>

js数组去重
------
以下是数组去重的三种方法：

    Array.prototype.unique1 = function () {
      var n = []; //一个新的临时数组
      for (var i = 0; i < this.length; i++) //遍历当前数组
      {
        //如果当前数组的第i已经保存进了临时数组，那么跳过，
        //否则把当前项push到临时数组里面
        if (n.indexOf(this[i]) == -1) n.push(this[i]);
      }
      return n;
    }
    
    Array.prototype.unique2 = function()
    {
    	var n = {},r=[]; //n为hash表，r为临时数组
    	for(var i = 0; i < this.length; i++) //遍历当前数组
    	{
    		if (!n[this[i]]) //如果hash表中没有当前项
    		{
    			n[this[i]] = true; //存入hash表
    			r.push(this[i]); //把当前数组的当前项push到临时数组里面
    		}
    	}
    	return r;
    }
    
    Array.prototype.unique3 = function()
    {
    	var n = [this[0]]; //结果数组
    	for(var i = 1; i < this.length; i++) //从第二项开始遍历
    	{
    		//如果当前数组的第i项在当前数组中第一次出现的位置不是i，
    		//那么表示第i项是重复的，忽略掉。否则存入结果数组
    		if (this.indexOf(this[i]) == i) n.push(this[i]);
    	}
    	return n;
    }
    

HTTP状态码
-------

    100  Continue  继续，一般在发送post请求时，已发送了http header之后服务端将返回此信息，表示确认，之后发送具体参数信息
    200  OK   正常返回信息
    201  Created  请求成功并且服务器创建了新的资源
    202  Accepted  服务器已接受请求，但尚未处理
    301  Moved Permanently  请求的网页已永久移动到新位置。
    302 Found  临时性重定向。
    303 See Other  临时性重定向，且总是使用 GET 请求新的 URI。
    304  Not Modified  自从上次请求后，请求的网页未修改过。
    
    400 Bad Request  服务器无法理解请求的格式，客户端不应当尝试再次使用相同的内容发起请求。
    401 Unauthorized  请求未授权。
    403 Forbidden  禁止访问。
    404 Not Found  找不到如何与 URI 相匹配的资源。
    
    500 Internal Server Error  最常见的服务器端错误。
    503 Service Unavailable 服务器端暂时无法处理请求（可能是过载或维护）。



js操作获取和设置cookie
---------------

    
    //创建cookie
    function setCookie(name, value, expires, path, domain, secure) {
    	var cookieText = encodeURIComponent(name) + '=' + encodeURIComponent(value);
    	if (expires instanceof Date) {
    		cookieText += '; expires=' + expires;
    	}
    	if (path) {
    		cookieText += '; expires=' + expires;
    	}
    	if (domain) {
    		cookieText += '; domain=' + domain;
    	}
    	if (secure) {
    		cookieText += '; secure';
    	}
    	document.cookie = cookieText;
    }
    
    //获取cookie
    function getCookie(name) {
    	var cookieName = encodeURIComponent(name) + '=';
    	var cookieStart = document.cookie.indexOf(cookieName);
    	var cookieValue = null;
    	if (cookieStart > -1) {
    		var cookieEnd = document.cookie.indexOf(';', cookieStart);
    		if (cookieEnd == -1) {
    			cookieEnd = document.cookie.length;
    		}
    		cookieValue = decodeURIComponent(document.cookie.substring(cookieStart + cookieName.length, cookieEnd));
    	}
    	return cookieValue;
    }
    
    //删除cookie
    function unsetCookie(name) {
    	document.cookie = name + "= ; expires=" + new Date(0);
    }

 
###说说TCP传输的三次握手策略

	为了准确无误地把数据送达目标处，TCP协议采用了三次握手策略。用TCP协议把数据包送出去后，TCP不会对传送  后的情况置之不理，它一定会向对方确认是否成功送达。握手过程中使用了TCP的标志：SYN和ACK。
	发送端首先发送一个带SYN标志的数据包给对方。接收端收到后，回传一个带有SYN/ACK标志的数据包以示传达确认信息。最后，发送端再回传一个带ACK标志的数据包，代表“握手”结束
	若在握手过程中某个阶段莫名中断，TCP协议会再次以相同的顺序发送相同的数据包。


###说说你对Promise的理解

依照 `Promise/A+` 的定义，`Promise` 有四种状态：

	pending: 初始状态, 非 fulfilled 或 rejected.
	fulfilled: 成功的操作.
	rejected: 失败的操作.
	settled: Promise已被fulfilled或rejected，且不是pending

另外， `fulfilled` 与 `rejected` 一起合称 `settled`。

`Promise` 对象用来进行延迟(deferred) 和异步(asynchronous ) 计算。

>Promise 的构造函数

构造一个 `Promise`，最基本的用法如下：

	var promise = new Promise(function(resolve, reject) {
	    if (...) {  // succeed
	        resolve(result);
	    } else {   // fails
	        reject(Error(errMessage));
	    }
	});

`Promise` 实例拥有 `then` 方法（具有 `then` 方法的对象，通常被称为 `thenable`）。它的使用方法如下：

	promise.then(onFulfilled, onRejected)

接收两个函数作为参数，一个在 `fulfilled` 的时候被调用，一个在 `rejected` 的时候被调用，接收参数就是 `future，onFulfilled` 对应 `resolve`, `onRejected` 对应 `reject`。


##Javascript垃圾回收方法

###标记清除（mark and sweep）


这是`JavaScript`最常见的垃圾回收方式，当变量进入执行环境的时候，比如函数中声明一个变量，垃圾回收器将其标记为“进入环境”，当变量离开环境的时候（函数执行结束）将其标记为“离开环境”。

垃圾回收器会在运行的时候给存储在内存中的所有变量加上标记，然后去掉环境中的变量以及被环境中变量所引用的变量（闭包），在这些完成之后仍存在标记的就是要删除的变量了

###引用计数(reference counting)

在低版本`IE`中经常会出现内存泄露，很多时候就是因为其采用引用计数方式进行垃圾回收。引用计数的策略是跟踪记录每个值被使用的次数，当声明了一个 变量并将一个引用类型赋值给该变量的时候这个值的引用次数就加1，如果该变量的值变成了另外一个，则这个值得引用次数减1，当这个值的引用次数变为0的时 候，说明没有变量在使用，这个值没法被访问了，因此可以将其占用的空间回收，这样垃圾回收器会在运行的时候清理掉引用次数为0的值占用的空间。

在IE中虽然`JavaScript`对象通过标记清除的方式进行垃圾回收，但BOM与DOM对象却是通过引用计数回收垃圾的，也就是说只要涉及BOM及DOM就会出现循环引用问题。

###谈谈性能优化问题

代码层面：避免使用css表达式，避免使用高级选择器，通配选择器。
缓存利用：缓存Ajax，使用CDN，使用外部js和css文件以便缓存，添加Expires头，服务端配置Etag，减少DNS查找等
请求数量：合并样式和脚本，使用css图片精灵，初始首屏之外的图片资源按需加载，静态资源延迟加载。
请求带宽：压缩文件，开启GZIP，

###移动端性能优化

>尽量使用`css3`动画，开启硬件加速。适当使用`touch`事件代替`click`事件。避免使用`css3`渐变阴影效果。
>尽可能少的使用`box-shadow`与`gradients`。`box-shadow`与`gradients`往往都是页面的性能杀手

##什么是Etag？

浏览器下载组件的时候，会将它们存储到浏览器缓存中。如果需要再次获取相同的组件，浏览器将检查组件的缓存时间，
假如已经过期，那么浏览器将发送一个条件GET请求到服务器，服务器判断缓存还有效，则发送一个304响应，
告诉浏览器可以重用缓存组件。

那么服务器是根据什么判断缓存是否还有效呢?答案有两种方式，一种是前面提到的ETag，另一种是根据`Last-Modified`

###Expires和Cache-Control

`Expires`要求客户端和服务端的时钟严格同步。HTTP1.1引入`Cache-Control`来克服Expires头的限制。如果max-age和Expires同时出现，则max-age有更高的优先级。

    Cache-Control: no-cache, private, max-age=0
    ETag: abcde
    Expires: Thu, 15 Apr 2014 20:00:00 GMT
    Pragma: private
    Last-Modified: $now // RFC1123 format

###栈和队列的区别?

    栈的插入和删除操作都是在一端进行的，而队列的操作却是在两端进行的。
    队列先进先出，栈先进后出。
    栈只允许在表尾一端进行插入和删除，而队列只允许在表尾一端进行插入，在表头一端进行删除 

###栈和堆的区别？

    栈区（stack）—   由编译器自动分配释放   ，存放函数的参数值，局部变量的值等。
    堆区（heap）   —   一般由程序员分配释放，   若程序员不释放，程序结束时可能由OS回收。
    堆（数据结构）：堆可以被看成是一棵树，如：堆排序；
    栈（数据结构）：一种先进后出的数据结构。 

###关于Http 2.0 你知道多少？

`HTTP/2`引入了“服务端推（serverpush）”的概念，它允许服务端在客户端需要数据之前就主动地将数据发送到客户端缓存中，从而提高性能。
`HTTP/2`提供更多的加密支持
`HTTP/2`使用多路技术，允许多个消息在一个连接上同时交差。 
它增加了头压缩（header compression），因此即使非常小的请求，其请求和响应的`header`都只会占用很小比例的带宽。
  
  下面是菜鸟网站的：
  
  本文收集总结了一些前端面试题，初学者阅后也要用心钻研其中的原理，重要知识需要系统学习、透彻学习，形成自己的知识链。万不可投机取巧，临时抱佛脚只求面试侥幸混过关是错误的！也是不可能的！不可能的！不可能的！

前端还是一个年轻的行业，新的行业标准， 框架， 库都不断在更新和新增，正如赫门在2015深JS大会上的《前端服务化之路》主题演讲中说的一句话："每18至24个月，前端都会难一倍"，这些变化使前端的能力更加丰富、创造的应用也会更加完美。所以关注各种前端技术，跟上快速变化的节奏，也是身为一个前端程序员必备的技能之一。

最近也收到许多微博私信的鼓励和更正题目信息，后面会经常更新题目和答案到github博客。希望前端er达到既能使用也会表达，对理论知识有自己的理解。可根据下面的知识点一个一个去进阶学习，形成自己的职业技能链。

面试有几点需注意：(来源寒冬winter 老师，github:@wintercn)
面试题目： 根据你的等级和职位的变化，入门级到专家级，广度和深度都会有所增加。
题目类型： 理论知识、算法、项目细节、技术视野、开放性题、工作案例。
细节追问： 可以确保问到你开始不懂或面试官开始不懂为止，这样可以大大延展题目的区分度和深度，知道你的实际能力。因为这种知识关联是长时期的学习，临时抱佛脚绝对是记不住的。
回答问题再棒，面试官（可能是你面试职位的直接领导），会考虑我要不要这个人做我的同事？所以态度很重要、除了能做事，还要会做人。（感觉更像是相亲( •̣̣̣̣̣̥́௰•̣̣̣̣̣̥̀ )）
资深的前端开发能把absolute和relative弄混，这样的人不要也罢，因为团队需要的是：你这个人具有可以依靠的才能（靠谱）。
前端开发知识点：
HTML&CSS：
    对Web标准的理解、浏览器内核差异、兼容性、hack、CSS基本功：布局、盒子模型、选择器优先级、
    HTML5、CSS3、Flexbox

JavaScript：
    数据类型、运算、对象、Function、继承、闭包、作用域、原型链、事件、RegExp、JSON、Ajax、
    DOM、BOM、内存泄漏、跨域、异步装载、模板引擎、前端MVC、路由、模块化、Canvas、ECMAScript 6、Nodejs

其他：
    移动端、响应式、自动化构建、HTTP、离线存储、WEB安全、优化、重构、团队协作、可维护、易用性、SEO、UED、架构、职业生涯、快速学习能力
作为一名前端工程师，无论工作年头长短都应该掌握的知识点：
此条由 王子墨 发表在 攻城师的实验室
 1、DOM结构 —— 两个节点之间可能存在哪些关系以及如何在节点之间任意移动。

    2、DOM操作 —— 如何添加、移除、移动、复制、创建和查找节点等。

    3、事件 —— 如何使用事件，以及IE和标准DOM事件模型之间存在的差别。

    4、XMLHttpRequest —— 这是什么、怎样完整地执行一次GET请求、怎样检测错误。

    5、严格模式与混杂模式 —— 如何触发这两种模式，区分它们有何意义。

    6、盒模型 —— 外边距、内边距和边框之间的关系，及IE8以下版本的浏览器中的盒模型

    7、块级元素与行内元素 —— 怎么用CSS控制它们、以及如何合理的使用它们

    8、浮动元素 —— 怎么使用它们、它们有什么问题以及怎么解决这些问题。

    9、HTML与XHTML —— 二者有什么区别，你觉得应该使用哪一个并说出理由。

    10、JSON —— 作用、用途、设计结构。
备注：
根据自己需要选择性阅读，面试题是对理论知识的总结，让自己学会应该如何表达。

资料答案不够正确和全面，欢迎欢迎Star和提交issues。

格式不断修改更新中。

更新记录：
2016年3月25日：新增ECMAScript6 相关问题
更新时间: 2016-3-25
HTML
Doctype作用？标准模式与兼容模式各有什么区别?
（1）、<!DOCTYPE>声明位于位于HTML文档中的第一行，处于 <html> 标签之前。告知浏览器的解析器用什么文档标准解析这个文档。DOCTYPE不存在或格式不正确会导致文档以兼容模式呈现。

（2）、标准模式的排版 和JS运作模式都是以该浏览器支持的最高标准运行。在兼容模式中，页面以宽松的向后兼容的方式显示,模拟老式浏览器的行为以防止站点无法工作。
HTML5 为什么只需要写 <!DOCTYPE HTML>？
HTML5 不基于 SGML，因此不需要对DTD进行引用，但是需要doctype来规范浏览器的行为（让浏览器按照它们应该的方式来运行）；

 而HTML4.01基于SGML,所以需要对DTD进行引用，才能告知浏览器文档所使用的文档类型。
行内元素有哪些？块级元素有哪些？ 空(void)元素有那些？
首先：CSS规范规定，每个元素都有display属性，确定该元素的类型，每个元素都有默认的display值，如div的display默认值为“block”，则为“块级”元素；span默认display属性值为“inline”，是“行内”元素。

（1）行内元素有：a b span img input select strong（强调的语气）
（2）块级元素有：div ul ol li dl dt dd h1 h2 h3 h4…p

（3）常见的空元素：
    <br> <hr> <img> <input> <link> <meta>
    鲜为人知的是：
    <area> <base> <col> <command> <embed> <keygen> <param> <source> <track> <wbr>
页面导入样式时，使用link和@import有什么区别？
（1）link属于XHTML标签，除了加载CSS外，还能用于定义RSS, 定义rel连接属性等作用；而@import是CSS提供的，只能用于加载CSS;

（2）页面被加载的时，link会同时被加载，而@import引用的CSS会等到页面被加载完再加载;

（3）import是CSS2.1 提出的，只在IE5以上才能被识别，而link是XHTML标签，无兼容问题;
介绍一下你对浏览器内核的理解？
主要分成两部分：渲染引擎(layout engineer或Rendering Engine)和JS引擎。
渲染引擎：负责取得网页的内容（HTML、XML、图像等等）、整理讯息（例如加入CSS等），以及计算网页的显示方式，然后会输出至显示器或打印机。浏览器的内核的不同对于网页的语法解释会有不同，所以渲染的效果也不相同。所有网页浏览器、电子邮件客户端以及其它需要编辑、显示网络内容的应用程序都需要内核。

JS引擎则：解析和执行javascript来实现网页的动态效果。

最开始渲染引擎和JS引擎并没有区分的很明确，后来JS引擎越来越独立，内核就倾向于只指渲染引擎。
常见的浏览器内核有哪些？
Trident内核：IE,MaxThon,TT,The World,360,搜狗浏览器等。[又称MSHTML]
Gecko内核：Netscape6及以上版本，FF,MozillaSuite/SeaMonkey等
Presto内核：Opera7及以上。      [Opera内核原为：Presto，现为：Blink;]
Webkit内核：Safari,Chrome等。   [ Chrome的：Blink（WebKit的分支）]
详细文章：浏览器内核的解析和对比
html5有哪些新特性、移除了那些元素？如何处理HTML5新标签的浏览器兼容问题？如何区分 HTML 和 HTML5？
* HTML5 现在已经不是 SGML 的子集，主要是关于图像，位置，存储，多任务等功能的增加。
      绘画 canvas;
      用于媒介回放的 video 和 audio 元素;
      本地离线存储 localStorage 长期存储数据，浏览器关闭后数据不丢失;
      sessionStorage 的数据在浏览器关闭后自动删除;
      语意化更好的内容元素，比如 article、footer、header、nav、section;
      表单控件，calendar、date、time、email、url、search;
      新的技术webworker, websocket, Geolocation;

  移除的元素：
      纯表现的元素：basefont，big，center，font, s，strike，tt，u;
      对可用性产生负面影响的元素：frame，frameset，noframes；

* 支持HTML5新标签：
     IE8/IE7/IE6支持通过document.createElement方法产生的标签，
     可以利用这一特性让这些浏览器支持HTML5新标签，
     浏览器支持新标签后，还需要添加标签默认的样式。

     当然也可以直接使用成熟的框架、比如html5shim;
     <!--[if lt IE 9]>
        <script> src="http://html5shim.googlecode.com/svn/trunk/html5.js"</script>
     <![endif]-->

* 如何区分HTML5： DOCTYPE声明\新增的结构元素\功能元素
简述一下你对HTML语义化的理解？
用正确的标签做正确的事情。
html语义化让页面的内容结构化，结构更清晰，便于对浏览器、搜索引擎解析;
即使在没有样式CSS情况下也以一种文档格式显示，并且是容易阅读的;
搜索引擎的爬虫也依赖于HTML标记来确定上下文和各个关键字的权重，利于SEO;
使阅读源代码的人对网站更容易将网站分块，便于阅读维护理解。
HTML5的离线储存怎么使用，工作原理能不能解释一下？
在用户没有与因特网连接时，可以正常访问站点或应用，在用户与因特网连接时，更新用户机器上的缓存文件。
原理：HTML5的离线存储是基于一个新建的.appcache文件的缓存机制(不是存储技术)，通过这个文件上的解析清单离线存储资源，这些资源就会像cookie一样被存储了下来。之后当网络在处于离线状态下时，浏览器会通过被离线存储的数据进行页面展示。


如何使用：
1、页面头部像下面一样加入一个manifest的属性；
2、在cache.manifest文件的编写离线存储的资源；
    CACHE MANIFEST
    #v0.11
    CACHE:
    js/app.js
    css/style.css
    NETWORK:
    resourse/logo.png
    FALLBACK:
    / /offline.html
3、在离线状态时，操作window.applicationCache进行需求实现。
详细的使用请参考：有趣的HTML5：离线存储
浏览器是怎么对HTML5的离线储存资源进行管理和加载的呢？
在线的情况下，浏览器发现html头部有manifest属性，它会请求manifest文件，如果是第一次访问app，那么浏览器就会根据manifest文件的内容下载相应的资源并且进行离线存储。如果已经访问过app并且资源已经离线存储了，那么浏览器就会使用离线的资源加载页面，然后浏览器会对比新的manifest文件与旧的manifest文件，如果文件没有发生改变，就不做任何操作，如果文件改变了，那么就会重新下载文件中的资源并进行离线存储。
离线的情况下，浏览器就直接使用离线存储的资源。
详细的使用请参考：有趣的HTML5：离线存储
请描述一下 cookies，sessionStorage 和 localStorage 的区别？
cookie是网站为了标示用户身份而储存在用户本地终端（Client Side）上的数据（通常经过加密）。
cookie数据始终在同源的http请求中携带（即使不需要），记会在浏览器和服务器间来回传递。
sessionStorage和localStorage不会自动把数据发给服务器，仅在本地保存。

存储大小：
    cookie数据大小不能超过4k。
    sessionStorage和localStorage 虽然也有存储大小的限制，但比cookie大得多，可以达到5M或更大。

有期时间：
    localStorage    存储持久数据，浏览器关闭后数据不丢失除非主动删除数据；
    sessionStorage  数据在当前浏览器窗口关闭后自动删除。
    cookie          设置的cookie过期时间之前一直有效，即使窗口或浏览器关闭
iframe有那些缺点？
*iframe会阻塞主页面的Onload事件；
*搜索引擎的检索程序无法解读这种页面，不利于SEO;

*iframe和主页面共享连接池，而浏览器对相同域的连接有限制，所以会影响页面的并行加载。

使用iframe之前需要考虑这两个缺点。如果需要使用iframe，最好是通过javascript
动态给iframe添加src属性值，这样可以绕开以上两个问题。
Label的作用是什么？是怎么用的？
label标签来定义表单控制间的关系,当用户选择该标签时，浏览器会自动将焦点转到和标签相关的表单控件上。

<label for="Name">Number:</label>
<input type=“text“name="Name" id="Name"/>

<label>Date:<input type="text" name="B"/></label>
HTML5的form如何关闭自动完成功能？
给不想要提示的 form 或某个 input 设置为 autocomplete=off。
如何实现浏览器内多个标签页之间的通信? (阿里)
WebSocket、SharedWorker；
也可以调用localstorge、cookies等本地存储方式；

localstorge另一个浏览上下文里被添加、修改或删除时，它都会触发一个事件，
我们通过监听事件，控制它的值来进行页面信息通信；
注意quirks：Safari 在无痕模式下设置localstorge值时会抛出 QuotaExceededError 的异常；
webSocket如何兼容低浏览器？(阿里)
Adobe Flash Socket 、
ActiveX HTMLFile (IE) 、
基于 multipart 编码发送 XHR 、
基于长轮询的 XHR
页面可见性（Page Visibility API） 可以有哪些用途？
通过 visibilityState 的值检测页面当前是否可见，以及打开网页的时间等;
在页面被切换到其他后台进程的时候，自动暂停音乐或视频的播放；
如何在页面上实现一个圆形的可点击区域？
1、map+area或者svg
2、border-radius
3、纯js实现 需要求一个点在不在圆上简单算法、获取鼠标坐标等等
实现不使用 border 画出1px高的线，在不同浏览器的标准模式与怪异模式下都能保持一致的效果。
<div style="height:1px;overflow:hidden;background:red"></div>
网页验证码是干嘛的，是为了解决什么安全问题。
区分用户是计算机还是人的公共全自动程序。可以防止恶意破解密码、刷票、论坛灌水；
有效防止黑客对某一个特定注册用户用特定程序暴力破解方式进行不断的登陆尝试。
title与h1的区别、b与strong的区别、i与em的区别？
title属性没有明确意义只表示是个标题，H1则表示层次明确的标题，对页面信息的抓取也有很大的影响；

strong是标明重点内容，有语气加强的含义，使用阅读设备阅读网络时：<strong>会重读，而<B>是展示强调内容。

i内容展示为斜体，em表示强调的文本；

Physical Style Elements -- 自然样式标签
b, i, u, s, pre
Semantic Style Elements -- 语义样式标签
strong, em, ins, del, code
应该准确使用语义样式标签, 但不能滥用, 如果不能确定时首选使用自然样式标签。
CSS
介绍一下标准的CSS的盒子模型？低版本IE的盒子模型有什么不同的？
（1）有两种， IE 盒子模型、W3C 盒子模型；
（2）盒模型： 内容(content)、填充(padding)、边界(margin)、 边框(border)；
（3）区  别： IE的content部分把 border 和 padding计算了进去;
CSS选择符有哪些？哪些属性可以继承？
*   1.id选择器（ # myid）
    2.类选择器（.myclassname）
    3.标签选择器（div, h1, p）
    4.相邻选择器（h1 + p）
    5.子选择器（ul > li）
    6.后代选择器（li a）
    7.通配符选择器（ * ）
    8.属性选择器（a[rel = "external"]）
    9.伪类选择器（a:hover, li:nth-child）

*   可继承的样式： font-size font-family color, UL LI DL DD DT;

*   不可继承的样式：border padding margin width height ;
CSS优先级算法如何计算？
*   优先级就近原则，同权重情况下样式定义最近者为准;

*   载入样式以最后载入的定位为准;

优先级为:
   !important >  id > class > tag
    important 比 内联优先级高
CSS3新增伪类有那些？
举例：
    p:first-of-type 选择属于其父元素的首个 <p> 元素的每个 <p> 元素。
    p:last-of-type  选择属于其父元素的最后 <p> 元素的每个 <p> 元素。
    p:only-of-type  选择属于其父元素唯一的 <p> 元素的每个 <p> 元素。
    p:only-child        选择属于其父元素的唯一子元素的每个 <p> 元素。
    p:nth-child(2)  选择属于其父元素的第二个子元素的每个 <p> 元素。

    :after          在元素之前添加内容,也可以用来做清除浮动。
    :before         在元素之后添加内容
    :enabled        
    :disabled       控制表单控件的禁用状态。
    :checked        单选框或复选框被选中。
如何居中div？如何居中一个浮动元素？如何让绝对定位的div居中？
给div设置一个宽度，然后添加margin:0 auto属性
div{
    width:200px;
    margin:0 auto;
 }
居中一个浮动元素
  确定容器的宽高 宽500 高 300 的层
  设置层的外边距

 .div {
      width:500px ; height:300px;//高度可以不设
      margin: -150px 0 0 -250px;
      position:relative;         //相对定位
      background-color:pink;     //方便看效果
      left:50%;
      top:50%;
 }
让绝对定位的div居中
  position: absolute;
  width: 1200px;
  background: none;
  margin: 0 auto;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
display有哪些值？说明他们的作用。
  block         象块类型元素一样显示。
  none          缺省值。象行内元素类型一样显示。
  inline-block  象行内元素一样显示，但其内容象块类型元素一样显示。
  list-item     象块类型元素一样显示，并添加样式列表标记。
  table         此元素会作为块级表格来显示
  inherit       规定应该从父元素继承 display 属性的值
position的值relative和absolute定位原点是？
  absolute
    生成绝对定位的元素，相对于值不为 static的第一个父元素进行定位。
  fixed （老IE不支持）
    生成绝对定位的元素，相对于浏览器窗口进行定位。
  relative
    生成相对定位的元素，相对于其正常位置进行定位。
  static
    默认值。没有定位，元素出现在正常的流中（忽略 top, bottom, left, right z-index 声明）。
  inherit
    规定从父元素继承 position 属性的值。
CSS3有哪些新特性？
  新增各种CSS选择器  （: not(.input)：所有 class 不是“input”的节点）
  圆角           （border-radius:8px）
  多列布局        （multi-column layout）
  阴影和反射        （Shadow\Reflect）
  文字特效      （text-shadow、）
  文字渲染      （Text-decoration）
  线性渐变      （gradient）
  旋转          （transform）
  增加了旋转,缩放,定位,倾斜,动画，多背景
  transform:\scale(0.85,0.90)\ translate(0px,-30px)\ skew(-9deg,0deg)\Animation:
请解释一下CSS3的Flexbox（弹性盒布局模型）,以及适用场景？
 .
用纯CSS创建一个三角形的原理是什么？
把上、左、右三条边隐藏掉（颜色设为 transparent）
#demo {
  width: 0;
  height: 0;
  border-width: 20px;
  border-style: solid;
  border-color: transparent transparent red transparent;
}
一个满屏 品 字布局 如何设计?
简单的方式：
    上面的div宽100%，
    下面的两个div分别宽50%，
    然后用float或者inline使其不换行即可
经常遇到的浏览器的兼容性有哪些？原因，解决方法是什么，常用hack的技巧 ？
* png24位的图片在iE6浏览器上出现背景，解决方案是做成PNG8.

* 浏览器默认的margin和padding不同。解决方案是加一个全局的*{margin:0;padding:0;}来统一。

* IE6双边距bug:块属性标签float后，又有横行的margin情况下，在ie6显示margin比设置的大。

  浮动ie产生的双倍距离 #box{ float:left; width:10px; margin:0 0 0 100px;}

  这种情况之下IE会产生20px的距离，解决方案是在float的标签样式控制中加入 ——_display:inline;将其转化为行内属性。(_这个符号只有ie6会识别)

  渐进识别的方式，从总体中逐渐排除局部。

  首先，巧妙的使用“\9”这一标记，将IE游览器从所有情况中分离出来。
  接着，再次使用“+”将IE8和IE7、IE6分离开来，这样IE8已经独立识别。

  css
      .bb{
          background-color:#f1ee18;/*所有识别*/
          .background-color:#00deff\9; /*IE6、7、8识别*/
          +background-color:#a200ff;/*IE6、7识别*/
          _background-color:#1e0bd1;/*IE6识别*/
      }

*  IE下,可以使用获取常规属性的方法来获取自定义属性,
   也可以使用getAttribute()获取自定义属性;
   Firefox下,只能使用getAttribute()获取自定义属性。
   解决方法:统一通过getAttribute()获取自定义属性。

*  IE下,even对象有x,y属性,但是没有pageX,pageY属性;
   Firefox下,event对象有pageX,pageY属性,但是没有x,y属性。

*  解决方法：（条件注释）缺点是在IE浏览器下可能会增加额外的HTTP请求数。

*  Chrome 中文界面下默认会将小于 12px 的文本强制按照 12px 显示,
   可通过加入 CSS 属性 -webkit-text-size-adjust: none; 解决。

超链接访问过后hover样式就不出现了 被点击访问过的超链接样式不在具有hover和active了解决方法是改变CSS属性的排列顺序:
L-V-H-A :  a:link {} a:visited {} a:hover {} a:active {}
li与li之间有看不见的空白间隔是什么原因引起的？有什么解决办法？
行框的排列会受到中间空白（回车\空格）等的影响，因为空格也属于字符,这些空白也会被应用样式，占据空间，所以会有间隔，把字符大小设为0，就没有空格了。
为什么要初始化CSS样式。
- 因为浏览器的兼容问题，不同浏览器对有些标签的默认值是不同的，如果没对CSS初始化往往会出现浏览器之间的页面显示差异。

- 当然，初始化样式会对SEO有一定的影响，但鱼和熊掌不可兼得，但力求影响最小的情况下初始化。

最简单的初始化方法： * {padding: 0; margin: 0;} （强烈不建议）

淘宝的样式初始化代码：
body, h1, h2, h3, h4, h5, h6, hr, p, blockquote, dl, dt, dd, ul, ol, li, pre, form, fieldset, legend, button, input, textarea, th, td { margin:0; padding:0; }
body, button, input, select, textarea { font:12px/1.5tahoma, arial, \5b8b\4f53; }
h1, h2, h3, h4, h5, h6{ font-size:100%; }
address, cite, dfn, em, var { font-style:normal; }
code, kbd, pre, samp { font-family:couriernew, courier, monospace; }
small{ font-size:12px; }
ul, ol { list-style:none; }
a { text-decoration:none; }
a:hover { text-decoration:underline; }
sup { vertical-align:text-top; }
sub{ vertical-align:text-bottom; }
legend { color:#000; }
fieldset, img { border:0; }
button, input, select, textarea { font-size:100%; }
table { border-collapse:collapse; border-spacing:0; }
absolute的containing block(容器块)计算方式跟正常流有什么不同？
无论属于哪种，都要先找到其祖先元素中最近的 position 值不为 static 的元素，然后再判断：
1、若此元素为 inline 元素，则 containing block 为能够包含这个元素生成的第一个和最后一个 inline box 的 padding box (除 margin, border 外的区域) 的最小矩形；
2、否则,则由这个祖先元素的 padding box 构成。
如果都找不到，则为 initial containing block。

补充：
1. static(默认的)/relative：简单说就是它的父元素的内容框（即去掉padding的部分）
2. absolute: 向上找最近的定位为absolute/relative的元素
3. fixed: 它的containing block一律为根元素(html/body)，根元素也是initial containing block
CSS里的visibility属性有个collapse属性值是干嘛用的？在不同浏览器下以后什么区别？
position跟display、margin collapse、overflow、float这些特性相互叠加后会怎么样？
对BFC规范(块级格式化上下文：block formatting context)的理解？
（W3C CSS 2.1 规范中的一个概念,它是一个独立容器，决定了元素如何对其内容进行定位,以及与其他元素的关系和相互作用。）
 一个页面是由很多个 Box 组成的,元素的类型和 display 属性,决定了这个 Box 的类型。
 不同类型的 Box,会参与不同的 Formatting Context（决定如何渲染文档的容器）,因此Box内的元素会以不同的方式渲染,也就是说BFC内部的元素和外部的元素不会互相影响。
css定义的权重
以下是权重的规则：标签的权重为1，class的权重为10，id的权重为100，以下例子是演示各种定义的权重值：

/*权重为1*/
div{
}
/*权重为10*/
.class1{
}
/*权重为100*/
#id1{
}
/*权重为100+1=101*/
#id1 div{
}
/*权重为10+1=11*/
.class1 div{
}
/*权重为10+10+1=21*/
.class1 .class2 div{
}

如果权重相同，则最后定义的样式会起作用，但是应该避免这种情况出现
请解释一下为什么会出现浮动和什么时候需要清除浮动？清除浮动的方式
移动端的布局用过媒体查询吗？
使用 CSS 预处理器吗？喜欢那个？
SASS (SASS、LESS没有本质区别，只因为团队前端都是用的SASS)
CSS优化、提高性能的方法有哪些？
浏览器是怎样解析CSS选择器的？
在网页中的应该使用奇数还是偶数的字体？为什么呢？
margin和padding分别适合什么场景使用？
抽离样式模块怎么写，说出思路，有无实践经验？[阿里航旅的面试题]
元素竖向的百分比设定是相对于容器的高度吗？
全屏滚动的原理是什么？用到了CSS的那些属性？
什么是响应式设计？响应式设计的基本原理是什么？如何兼容低版本的IE？
视差滚动效果，如何给每页做不同的动画？（回到顶部，向下滑动要再次出现，和只出现一次分别怎么做？）
::before 和 :after中双冒号和单冒号 有什么区别？解释一下这2个伪元素的作用。
如何修改chrome记住密码后自动填充表单的黄色背景 ？
你对line-height是如何理解的？
设置元素浮动后，该元素的display值是多少？（自动变成display:block）
怎么让Chrome支持小于12px 的文字？
让页面里的字体变清晰，变细用CSS怎么做？（-webkit-font-smoothing: antialiased;）
font-style属性可以让它赋值为"oblique" oblique是什么意思？
position:fixed;在android下无效怎么处理？
如果需要手动写动画，你认为最小时间间隔是多久，为什么？（阿里）
多数显示器默认频率是60Hz，即1秒刷新60次，所以理论上最小间隔为1/60＊1000ms ＝ 16.7ms
display:inline-block 什么时候会显示间隙？(携程)
移除空格、使用margin负值、使用font-size:0、letter-spacing、word-spacing
overflow: scroll时不能平滑滚动的问题怎么处理？
有一个高度自适应的div，里面有两个div，一个高度100px，希望另一个填满剩下的高度。
png、jpg、gif 这些图片格式解释一下，分别什么时候用。有没有了解过webp？
什么是Cookie 隔离？（或者说：请求资源的时候不要让它带cookie怎么做）
如果静态文件都放在主域名下，那静态文件请求的时候都带有的cookie的数据提交给server的，非常浪费流量，
所以不如隔离开。

因为cookie有域的限制，因此不能跨域提交请求，故使用非主要域名的时候，请求头中就不会带有cookie数据，
这样可以降低请求头的大小，降低请求时间，从而达到降低整体请求延时的目的。

同时这种方式不会将cookie传入Web Server，也减少了Web Server对cookie的处理分析环节，
提高了webserver的http请求的解析速度。
style标签写在body后与body前有什么区别？
什么是CSS 预处理器 / 后处理器？
- 预处理器例如：LESS、Sass、Stylus，用来预编译Sass或less，增强了css代码的复用性，
  还有层级、mixin、变量、循环、函数等，具有很方便的UI组件模块化开发能力，极大的提高工作效率。

- 后处理器例如：PostCSS，通常被视为在完成的样式表中根据CSS规范处理CSS，让其更有效；目前最常做的
  是给CSS属性添加浏览器私有前缀，实现跨浏览器兼容性的问题。
JavaScript
介绍js的基本数据类型。
 Undefined、Null、Boolean、Number、String
介绍js有哪些内置对象？
Object 是 JavaScript 中所有对象的父对象

数据封装类对象：Object、Array、Boolean、Number 和 String
其他对象：Function、Arguments、Math、Date、RegExp、Error
说几条写JavaScript的基本规范？
1.不要在同一行声明多个变量。
2.请使用 ===/!==来比较true/false或者数值
3.使用对象字面量替代new Array这种形式
4.不要使用全局函数。
5.Switch语句必须带有default分支
6.函数不应该有时候有返回值，有时候没有返回值。
7.For循环必须使用大括号
8.If语句必须使用大括号
9.for-in循环中的变量 应该使用var关键字明确限定作用域，从而避免作用域污染。
JavaScript原型，原型链 ? 有什么特点？
每个对象都会在其内部初始化一个属性，就是prototype(原型)，当我们访问一个对象的属性时，
如果这个对象内部不存在这个属性，那么他就会去prototype里找这个属性，这个prototype又会有自己的prototype，
于是就这样一直找下去，也就是我们平时所说的原型链的概念。
关系：instance.constructor.prototype = instance.__proto__

特点：
JavaScript对象是通过引用来传递的，我们创建的每个新对象实体中并没有一份属于自己的原型副本。当我们修改原型时，与之相关的对象也会继承这一改变。


 当我们需要一个属性的时，Javascript引擎会先看当前对象中是否有这个属性， 如果没有的话，
 就会查找他的Prototype对象是否有这个属性，如此递推下去，一直检索到 Object 内建对象。
    function Func(){}
    Func.prototype.name = "Sean";
    Func.prototype.getInfo = function() {
      return this.name;
    }
    var person = new Func();//现在可以参考var person = Object.create(oldObject);
    console.log(person.getInfo());//它拥有了Func的属性和方法
    //"Sean"
    console.log(Func.prototype);
    // Func { name="Sean", getInfo=function()}
JavaScript有几种类型的值？，你能画一下他们的内存图吗？
栈：原始数据类型（Undefined，Null，Boolean，Number、String） 
堆：引用数据类型（对象、数组和函数）

两种类型的区别是：存储位置不同；
原始数据类型直接存储在栈(stack)中的简单数据段，占据空间小、大小固定，属于被频繁使用数据，所以放入栈中存储；
引用数据类型存储在堆(heap)中的对象,占据空间大、大小不固定,如果存储在栈中，将会影响程序运行的性能；引用数据类型在栈中存储了指针，该指针指向堆中该实体的起始地址。当解释器寻找引用值时，会首先检索其
在栈中的地址，取得地址后从堆中获得实体
Stated Clearly Image
Javascript如何实现继承？
1、构造继承
2、原型继承
3、实例继承
4、拷贝继承

原型prototype机制或apply和call方法去实现较简单，建议使用构造函数与原型混合方式。

 function Parent(){
        this.name = 'wang';
    }

    function Child(){
        this.age = 28;
    }
    Child.prototype = new Parent();//继承了Parent，通过原型

    var demo = new Child();
    alert(demo.age);
    alert(demo.name);//得到被继承的属性
  }
JavaScript继承的几种实现方式？
参考：构造函数的继承，非构造函数的继承；
javascript创建对象的几种方式？
javascript创建对象简单的说,无非就是使用内置对象或各种自定义对象，当然还可以用JSON；但写法有很多种，也能混合使用。


1、对象字面量的方式   

    person={firstname:"Mark",lastname:"Yun",age:25,eyecolor:"black"};

2、用function来模拟无参的构造函数

    function Person(){}
    var person=new Person();//定义一个function，如果使用new"实例化",该function可以看作是一个Class
    person.name="Mark";
    person.age="25";
    person.work=function(){
    alert(person.name+" hello...");
    }
    person.work();

3、用function来模拟参构造函数来实现（用this关键字定义构造的上下文属性）

    function Pet(name,age,hobby){
       this.name=name;//this作用域：当前对象
       this.age=age;
       this.hobby=hobby;
       this.eat=function(){
          alert("我叫"+this.name+",我喜欢"+this.hobby+",是个程序员");
       }
    }
    var maidou =new Pet("麦兜",25,"coding");//实例化、创建对象
    maidou.eat();//调用eat方法


4、用工厂方式来创建（内置对象）

     var wcDog =new Object();
     wcDog.name="旺财";
     wcDog.age=3;
     wcDog.work=function(){
       alert("我是"+wcDog.name+",汪汪汪......");
     }
     wcDog.work();


5、用原型方式来创建

    function Dog(){

     }
     Dog.prototype.name="旺财";
     Dog.prototype.eat=function(){
     alert(this.name+"是个吃货");
     }
     var wangcai =new Dog();
     wangcai.eat();


5、用混合方式来创建

    function Car(name,price){
      this.name=name;
      this.price=price; 
    }
     Car.prototype.sell=function(){
       alert("我是"+this.name+"，我现在卖"+this.price+"万元");
      }
    var camry =new Car("凯美瑞",27);
    camry.sell(); 
Javascript作用链域?
全局函数无法查看局部函数的内部细节，但局部函数可以查看其上层的函数细节，直至全局细节。
当需要从局部函数查找某一属性或方法时，如果当前作用域没有找到，就会上溯到上层作用域查找，
直至全局函数，这种组织形式就是作用域链。
谈谈This对象的理解。
this总是指向函数的直接调用者（而非间接调用者）；
如果有new关键字，this指向new出来的那个对象；
在事件中，this指向触发这个事件的对象，特殊的是，IE中的attachEvent中的this总是指向全局对象Window；
eval是做什么的？
它的功能是把对应的字符串解析成JS代码并运行；
应该避免使用eval，不安全，非常耗性能（2次，一次解析成js语句，一次执行）。
由JSON字符串转换为JSON对象的时候可以用eval，var obj =eval('('+ str +')');
什么是window对象? 什么是document对象?
null，undefined 的区别？
null        表示一个对象被定义了，值为“空值”；
undefined   表示不存在这个值。


typeof undefined
    //"undefined"
    undefined :是一个表示"无"的原始值或者说表示"缺少值"，就是此处应该有一个值，但是还没有定义。当尝试读取时会返回 undefined； 
    例如变量被声明了，但没有赋值时，就等于undefined

typeof null
    //"object"
    null : 是一个对象(空对象, 没有任何属性和方法)；
    例如作为函数的参数，表示该函数的参数不是对象；

注意：
    在验证null时，一定要使用　=== ，因为 == 无法分别 null 和　undefined


再来一个例子：

    null
    Q：有张三这个人么？
    A：有！
    Q：张三有房子么？
    A：没有！

    undefined
    Q：有张三这个人么？
    A：没有！
参考阅读：undefined与null的区别
写一个通用的事件侦听器函数。
    // event(事件)工具集，来源：github.com/markyun
    markyun.Event = {
        // 页面加载完成后
        readyEvent : function(fn) {
            if (fn==null) {
                fn=document;
            }
            var oldonload = window.onload;
            if (typeof window.onload != 'function') {
                window.onload = fn;
            } else {
                window.onload = function() {
                    oldonload();
                    fn();
                };
            }
        },
        // 视能力分别使用dom0||dom2||IE方式 来绑定事件
        // 参数： 操作的元素,事件名称 ,事件处理程序
        addEvent : function(element, type, handler) {
            if (element.addEventListener) {
                //事件类型、需要执行的函数、是否捕捉
                element.addEventListener(type, handler, false);
            } else if (element.attachEvent) {
                element.attachEvent('on' + type, function() {
                    handler.call(element);
                });
            } else {
                element['on' + type] = handler;
            }
        },
        // 移除事件
        removeEvent : function(element, type, handler) {
            if (element.removeEventListener) {
                element.removeEventListener(type, handler, false);
            } else if (element.datachEvent) {
                element.detachEvent('on' + type, handler);
            } else {
                element['on' + type] = null;
            }
        },
        // 阻止事件 (主要是事件冒泡，因为IE不支持事件捕获)
        stopPropagation : function(ev) {
            if (ev.stopPropagation) {
                ev.stopPropagation();
            } else {
                ev.cancelBubble = true;
            }
        },
        // 取消事件的默认行为
        preventDefault : function(event) {
            if (event.preventDefault) {
                event.preventDefault();
            } else {
                event.returnValue = false;
            }
        },
        // 获取事件目标
        getTarget : function(event) {
            return event.target || event.srcElement;
        },
        // 获取event对象的引用，取到事件的所有信息，确保随时能使用event；
        getEvent : function(e) {
            var ev = e || window.event;
            if (!ev) {
                var c = this.getEvent.caller;
                while (c) {
                    ev = c.arguments[0];
                    if (ev && Event == ev.constructor) {
                        break;
                    }
                    c = c.caller;
                }
            }
            return ev;
        }
    };
["1", "2", "3"].map(parseInt) 答案是多少？
 [1, NaN, NaN] 因为 parseInt 需要两个参数 (val, radix)，
 其中 radix 表示解析时用的基数。
 map 传了 3 个 (element, index, array)，对应的 radix 不合法导致解析失败。
事件是？IE与火狐的事件机制有什么区别？ 如何阻止冒泡？
 1. 我们在网页中的某个操作（有的操作对应多个事件）。例如：当我们点击一个按钮就会产生一个事件。是可以被 JavaScript 侦测到的行为。
 2. 事件处理机制：IE是事件冒泡、Firefox同时支持两种事件模型，也就是：捕获型事件和冒泡型事件；
 3. ev.stopPropagation();（旧ie的方法 ev.cancelBubble = true;）
什么是闭包（closure），为什么要用它？
闭包是指有权访问另一个函数作用域中变量的函数，创建闭包的最常见的方式就是在一个函数内创建另一个函数，通过另一个函数访问这个函数的局部变量,利用闭包可以突破作用链域，将函数内部的变量和方法传递到外部。

闭包的特性：

1.函数内再嵌套函数
2.内部函数可以引用外层的参数和变量
3.参数和变量不会被垃圾回收机制回收

//li节点的onclick事件都能正确的弹出当前被点击的li索引
 <ul id="testUL">
    <li> index = 0</li>
    <li> index = 1</li>
    <li> index = 2</li>
    <li> index = 3</li>
</ul>
<script type="text/javascript">
    var nodes = document.getElementsByTagName("li");
    for(i = 0;i<nodes.length;i+= 1){
        nodes[i].onclick = function(){
            console.log(i+1);//不用闭包的话，值每次都是4
        }(i);
    }
</script>



执行say667()后,say667()闭包内部变量会存在,而闭包内部函数的内部变量不会存在
使得Javascript的垃圾回收机制GC不会收回say667()所占用的资源
因为say667()的内部函数的执行需要依赖say667()中的变量
这是对闭包作用的非常直白的描述

  function say667() {
    // Local variable that ends up within closure
    var num = 666;
    var sayAlert = function() {
        alert(num);
    }
    num++;
    return sayAlert;
}

 var sayAlert = say667();
 sayAlert()//执行结果应该弹出的667
javascript 代码中的"use strict";是什么意思 ? 使用它区别是什么？
use strict是一种ECMAscript 5 添加的（严格）运行模式,这种模式使得 Javascript 在更严格的条件下运行,

使JS编码更加规范化的模式,消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为。
默认支持的糟糕特性都会被禁用，比如不能用with，也不能在意外的情况下给全局变量赋值;
全局变量的显示声明,函数必须声明在顶层，不允许在非函数代码块内声明函数,arguments.callee也不允许使用；
消除代码运行的一些不安全之处，保证代码运行的安全,限制函数中的arguments修改，严格模式下的eval函数的行为和非严格模式的也不相同;

提高编译器效率，增加运行速度；
为未来新版本的Javascript标准化做铺垫。
如何判断一个对象是否属于某个类？
  使用instanceof （待完善）
   if(a instanceof Person){
       alert('yes');
   }
new操作符具体干了什么呢?
     1、创建一个空对象，并且 this 变量引用该对象，同时还继承了该函数的原型。
     2、属性和方法被加入到 this 引用的对象中。
     3、新创建的对象由 this 所引用，并且最后隐式的返回 this 。

var obj  = {};
obj.__proto__ = Base.prototype;
Base.call(obj);
用原生JavaScript的实现过什么功能吗？
Javascript中，有一个函数，执行时对象查找时，永远不会去查找原型，这个函数是？
hasOwnProperty

javaScript中hasOwnProperty函数方法是返回一个布尔值，指出一个对象是否具有指定名称的属性。此方法无法检查该对象的原型链中是否具有该属性；该属性必须是对象本身的一个成员。
使用方法：
object.hasOwnProperty(proName)
其中参数object是必选项。一个对象的实例。
proName是必选项。一个属性名称的字符串值。

如果 object 具有指定名称的属性，那么JavaScript中hasOwnProperty函数方法返回 true，反之则返回 false。
JSON 的了解？
JSON(JavaScript Object Notation) 是一种轻量级的数据交换格式。
它是基于JavaScript的一个子集。数据格式简单, 易于读写, 占用带宽小
如：{"age":"12", "name":"back"}

JSON字符串转换为JSON对象:
var obj =eval('('+ str +')');
var obj = str.parseJSON();
var obj = JSON.parse(str);

JSON对象转换为JSON字符串：
var last=obj.toJSONString();
var last=JSON.stringify(obj);
[].forEach.call($$("*"),function(a){a.style.outline="1px solid #"+(~~(Math.random()*(1<<24))).toString(16)}) 能解释一下这段代码的意思吗？
js延迟加载的方式有哪些？
defer和async、动态创建DOM方式（用得最多）、按需异步载入js
Ajax 是什么? 如何创建一个Ajax？
ajax的全称：Asynchronous Javascript And XML。
异步传输+js+xml。
所谓异步，在这里简单地解释就是：向服务器发送请求的时候，我们不必等待结果，而是可以同时做其他的事情，等到有了结果它自己会根据设定进行后续操作，与此同时，页面是不会发生整页刷新的，提高了用户体验。

(1)创建XMLHttpRequest对象,也就是创建一个异步调用对象
(2)创建一个新的HTTP请求,并指定该HTTP请求的方法、URL及验证信息
(3)设置响应HTTP请求状态变化的函数
(4)发送HTTP请求
(5)获取异步调用返回的数据
(6)使用JavaScript和DOM实现局部刷新
同步和异步的区别?
同步的概念应该是来自于OS中关于同步的概念:不同进程为协同完成某项工作而在先后次序上调整(通过阻塞,唤醒等方式).同步强调的是顺序性.谁先谁后.异步则不存在这种顺序性.
同步：浏览器访问服务器请求，用户看得到页面刷新，重新发请求,等请求完，页面刷新，新内容出现，用户看到新内容,进行下一步操作。
异步：浏览器访问服务器请求，用户正常操作，浏览器后端进行请求。等请求完，页面不刷新，新内容也会出现，用户看到新内容。
（待完善）
如何解决跨域问题?
jsonp、 iframe、window.name、window.postMessage、服务器上设置代理页面
页面编码和被请求的资源编码如果不一致如何处理？
模块化开发怎么做？
立即执行函数,不暴露私有成员
    var module1 = (function(){
    　　　　var _count = 0;
    　　　　var m1 = function(){
    　　　　　　//...
    　　　　};
    　　　　var m2 = function(){
    　　　　　　//...
    　　　　};
    　　　　return {
    　　　　　　m1 : m1,
    　　　　　　m2 : m2
    　　　　};
    　　})();
（待完善）
AMD（Modules/Asynchronous-Definition）、CMD（Common Module Definition）规范区别？
AMD 规范在这里：https://github.com/amdjs/amdjs-api/wiki/AMD
CMD 规范在这里：https://github.com/seajs/seajs/issues/242
Asynchronous Module Definition，异步模块定义，所有的模块将被异步加载，模块加载不影响后面语句运行。所有依赖某些模块的语句均放置在回调函数中。

 区别：

    1. 对于依赖的模块，AMD 是提前执行，CMD 是延迟执行。不过 RequireJS 从 2.0 开始，也改成可以延迟执行（根据写法不同，处理方式不同）。CMD 推崇 as lazy as possible.
    2. CMD 推崇依赖就近，AMD 推崇依赖前置。看代码：

// CMD
define(function(require, exports, module) {
    var a = require('./a')
    a.doSomething()
    // 此处略去 100 行
    var b = require('./b') // 依赖可以就近书写
    b.doSomething()
    // ...
})

// AMD 默认推荐
define(['./a', './b'], function(a, b) { // 依赖必须一开始就写好
    a.doSomething()
    // 此处略去 100 行
    b.doSomething()
    // ...
})
requireJS的核心原理是什么？（如何动态加载的？如何避免多次加载的？如何 缓存的？）
谈一谈你对ECMAScript6的了解？
ECMAScript6 怎么写class么，为什么会出现class这种东西?
异步加载JS的方式有哪些？
  (1) defer，只支持IE

  (2) async：

  (3) 创建script，插入到DOM中，加载完毕后callBack
documen.write和 innerHTML的区别
document.write只能重绘整个页面

innerHTML可以重绘页面的一部分
DOM操作——怎样添加、移除、移动、复制、创建和查找节点?
（1）创建新节点
  createDocumentFragment()    //创建一个DOM片段
  createElement()   //创建一个具体的元素
  createTextNode()   //创建一个文本节点
（2）添加、移除、替换、插入
  appendChild()
  removeChild()
  replaceChild()
  insertBefore() //在已有的子节点前插入一个新的子节点
（3）查找
  getElementsByTagName()    //通过标签名称
  getElementsByName()    //通过元素的Name属性的值(IE容错能力较强，会得到一个数组，其中包括id等于name值的)
  getElementById()    //通过元素Id，唯一性
.call() 和 .apply() 的区别？
  例子中用 add 来替换 sub，add.call(sub,3,1) == add(3,1) ，所以运行结果为：alert(4);

  注意：js 中的函数其实是对象，函数名是对 Function 对象的引用。

    function add(a,b)
    {
        alert(a+b);
    }

    function sub(a,b)
    {
        alert(a-b);
    }

    add.call(sub,3,1);
数组和对象有哪些原生方法，列举一下？
JS 怎么实现一个类。怎么实例化这个类
JavaScript中的作用域与变量声明提升？
如何编写高性能的Javascript？
那些操作会造成内存泄漏？
JQuery的源码看过吗？能不能简单概况一下它的实现原理？
jQuery.fn的init方法返回的this指的是什么对象？为什么要返回this？
jquery中如何将数组转化为json字符串，然后再转化回来？
jQuery 的属性拷贝(extend)的实现原理是什么，如何实现深拷贝？
jquery.extend 与 jquery.fn.extend的区别？
jQuery 的队列是如何实现的？队列可以用在哪些地方？
谈一下Jquery中的bind(),live(),delegate(),on()的区别？
JQuery一个对象可以同时绑定多个事件，这是如何实现的？
是否知道自定义事件。jQuery里的fire函数是什么意思，什么时候用？
jQuery 是通过哪个方法和 Sizzle 选择器结合的？（jQuery.fn.find()进入Sizzle）
针对 jQuery性能的优化方法？
Jquery与jQuery UI 有啥区别？
*jQuery是一个js库，主要提供的功能是选择器，属性修改和事件绑定等等。

*jQuery UI则是在jQuery的基础上，利用jQuery的扩展性，设计的插件。
 提供了一些常用的界面元素，诸如对话框、拖动行为、改变大小行为等等
JQuery的源码看过吗？能不能简单说一下它的实现原理？
jquery 中如何将数组转化为json字符串，然后再转化回来？
jQuery中没有提供这个功能，所以你需要先编写两个jQuery的扩展：
    $.fn.stringifyArray = function(array) {
        return JSON.stringify(array)
    }

    $.fn.parseArray = function(array) {
        return JSON.parse(array)
    }

    然后调用：
    $("").stringifyArray(array)
jQuery和Zepto的区别？各自的使用场景？
针对 jQuery 的优化方法？
*基于Class的选择性的性能相对于Id选择器开销很大，因为需遍历所有DOM元素。

*频繁操作的DOM，先缓存起来再操作。用Jquery的链式调用更好。
 比如：var str=$("a").attr("href");

*for (var i = size; i < arr.length; i++) {}
 for 循环每一次循环都查找了数组 (arr) 的.length 属性，在开始循环的时候设置一个变量来存储这个数字，可以让循环跑得更快：
 for (var i = size, length = arr.length; i < length; i++) {}
Zepto的点透问题如何解决？
jQueryUI如何自定义组件?
需求：实现一个页面操作不会整页刷新的网站，并且能在浏览器前进、后退时正确响应。给出你的技术实现方案？
如何判断当前脚本运行在浏览器还是node环境中？（阿里）
通过判断Global对象是否为window，如果不为window，当前脚本没有运行在浏览器中
移动端最小触控区域是多大？
jQuery 的 slideUp动画 ，如果目标元素是被外部事件驱动, 当鼠标快速地连续触发外部元素事件, 动画会滞后的反复执行，该如何处理呢?
把 Script 标签 放在页面的最底部的body封闭之前 和封闭之后有什么区别？浏览器会如何解析它们？
移动端的点击事件的有延迟，时间是多久，为什么会有？ 怎么解决这个延时？（click 有 300ms 延迟,为了实现safari的双击事件的设计，浏览器要知道你是不是要双击操作。）
知道各种JS框架(Angular, Backbone, Ember, React, Meteor, Knockout...)么? 能讲出他们各自的优点和缺点么?
Underscore 对哪些 JS 原生对象进行了扩展以及提供了哪些好用的函数方法？
解释JavaScript中的作用域与变量声明提升？
那些操作会造成内存泄漏？
内存泄漏指任何对象在您不再拥有或需要它之后仍然存在。
垃圾回收器定期扫描对象，并计算引用了每个对象的其他对象的数量。如果一个对象的引用数量为 0（没有其他对象引用过该对象），或对该对象的惟一引用是循环的，那么该对象的内存即可回收。

setTimeout 的第一个参数使用字符串而非函数的话，会引发内存泄漏。
闭包、控制台日志、循环（在两个对象彼此引用且彼此保留时，就会产生一个循环）
JQuery一个对象可以同时绑定多个事件，这是如何实现的？
Node.js的适用场景？
(如果会用node)知道route, middleware, cluster, nodemon, pm2, server-side rendering么?
解释一下 Backbone 的 MVC 实现方式？
什么是"前端路由"?什么时候适合使用"前端路由"? "前端路由"有哪些优点和缺点?
知道什么是webkit么? 知道怎么用浏览器的各种工具来调试和debug代码么?
如何测试前端代码么? 知道BDD, TDD, Unit Test么? 知道怎么测试你的前端工程么(mocha, sinon, jasmin, qUnit..)?
前端templating(Mustache, underscore, handlebars)是干嘛的, 怎么用?
简述一下 Handlebars 的基本用法？
简述一下 Handlerbars 的对模板的基本处理流程， 如何编译的？如何缓存的？
用js实现千位分隔符?(来源：前端农民工，提示：正则+replace)
function commafy(num) {
     num = num + '';
     var reg = /(-?d+)(d{3})/;

    if(reg.test(num)){
     num = num.replace(reg, '$1,$2');
    }
    return num;
}
检测浏览器版本版本有哪些方式？
功能检测、userAgent特征检测

比如：navigator.userAgent
//"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_2) AppleWebKit/537.36
  (KHTML, like Gecko) Chrome/41.0.2272.101 Safari/537.36"
What is a Polyfill?
polyfill 是“在旧版浏览器上复制标准 API 的 JavaScript 补充”,可以动态地加载 JavaScript 代码或库，在不支持这些标准 API 的浏览器中模拟它们。
例如，geolocation（地理位置）polyfill 可以在 navigator 对象上添加全局的 geolocation 对象，还能添加 getCurrentPosition 函数以及“坐标”回调对象，
所有这些都是 W3C 地理位置 API 定义的对象和函数。因为 polyfill 模拟标准 API，所以能够以一种面向所有浏览器未来的方式针对这些 API 进行开发，
一旦对这些 API 的支持变成绝对大多数，则可以方便地去掉 polyfill，无需做任何额外工作。
做的项目中，有没有用过或自己实现一些 polyfill 方案（兼容性处理方案）？
比如： html5shiv、Geolocation、Placeholder 
我们给一个dom同时绑定两个点击事件，一个用捕获，一个用冒泡。会执行几次事件，会先执行冒泡还是捕获？
ECMAScript6 相关
Object.is() 与原来的比较操作符" ==="、" =="的区别？
两等号判等，会在比较时进行类型转换；
三等号判等(判断严格)，比较时不进行隐式类型转换,（类型不同则会返回false）； 

Object.is 在三等号判等的基础上特别处理了 NaN 、-0 和 +0 ，保证 -0 和 +0 不再相同，
但 Object.is(NaN, NaN) 会返回 true.

Object.is 应被认为有其特殊的用途，而不能用它认为它比其它的相等对比更宽松或严格。
前端框架相关
react-router 路由系统的实现原理？
React中如何解决第三方类库的问题?
其他问题
原来公司工作流程是怎么样的，如何与其他人协作的？如何夸部门合作的？
你遇到过比较难的技术问题是？你是如何解决的？
设计模式 知道什么是singleton, factory, strategy, decrator么?
常使用的库有哪些？常用的前端开发工具？开发过什么应用或组件？
页面重构怎么操作？
网站重构：在不改变外部行为的前提下，简化结构、添加可读性，而在网站前端保持一致的行为。
也就是说是在不改变UI的情况下，对网站进行优化，在扩展的同时保持一致的UI。

对于传统的网站来说重构通常是：

表格(table)布局改为DIV+CSS
使网站前端兼容于现代浏览器(针对于不合规范的CSS、如对IE6有效的)
对于移动平台的优化
针对于SEO进行优化
深层次的网站重构应该考虑的方面

减少代码间的耦合
让代码保持弹性
严格按规范编写代码
设计可扩展的API
代替旧有的框架、语言(如VB)
增强用户体验
通常来说对于速度的优化也包含在重构中

压缩JS、CSS、image等前端资源(通常是由服务器来解决)
程序的性能优化(如数据读写)
采用CDN来加速资源加载
对于JS DOM的优化
HTTP服务器的文件缓存
列举IE与其他浏览器不一样的特性？
1、事件不同之处：

    触发事件的元素被认为是目标（target）。而在 IE 中，目标包含在 event 对象的 srcElement 属性；

    获取字符代码、如果按键代表一个字符（shift、ctrl、alt除外），IE 的 keyCode 会返回字符代码（Unicode），DOM 中按键的代码和字符是分离的，要获取字符代码，需要使用 charCode 属性；

    阻止某个事件的默认行为，IE 中阻止某个事件的默认行为，必须将 returnValue 属性设置为 false，Mozilla 中，需要调用 preventDefault() 方法；

    停止事件冒泡，IE 中阻止事件进一步冒泡，需要设置 cancelBubble 为 true，Mozzilla 中，需要调用 stopPropagation()；
99%的网站都需要被重构是那本书上写的？
网站重构：应用web标准进行设计（第2版）
什么叫优雅降级和渐进增强？
优雅降级：Web站点在所有新式浏览器中都能正常工作，如果用户使用的是老式浏览器，则代码会针对旧版本的IE进行降级处理了,使之在旧式浏览器上以某种形式降级体验却不至于完全不能用。
如：border-shadow

渐进增强：从被所有浏览器支持的基本功能开始，逐步地添加那些只有新版本浏览器才支持的功能,向页面增加不影响基础浏览器的额外样式和功能的。当浏览器支持时，它们会自动地呈现出来并发挥作用。
如：默认使用flash上传，但如果浏览器支持 HTML5 的文件上传功能，则使用HTML5实现更好的体验；
是否了解公钥加密和私钥加密。
一般情况下是指私钥用于对数据进行签名，公钥用于对签名进行验证;
HTTP网站在浏览器端用公钥加密敏感数据，然后在服务器端再用私钥解密。
WEB应用从服务器主动推送Data到客户端有那些方式？
html5提供的Websocket
不可见的iframe
WebSocket通过Flash
XHR长时间连接
XHR Multipart Streaming
<script>标签的长时间连接(可跨域)
对Node的优点和缺点提出了自己的看法？
*（优点）因为Node是基于事件驱动和无阻塞的，所以非常适合处理并发请求，
  因此构建在Node上的代理服务器相比其他技术实现（如Ruby）的服务器表现要好得多。
  此外，与Node代理服务器交互的客户端代码是由javascript语言编写的，
  因此客户端和服务器端都用同一种语言编写，这是非常美妙的事情。

*（缺点）Node是一个相对新的开源项目，所以不太稳定，它总是一直在变，
  而且缺少足够多的第三方库支持。看起来，就像是Ruby/Rails当年的样子。
你有用过哪些前端性能优化的方法？
  （1） 减少http请求次数：CSS Sprites, JS、CSS源码压缩、图片大小控制合适；网页Gzip，CDN托管，data缓存 ，图片服务器。

  （2） 前端模板 JS+数据，减少由于HTML标签导致的带宽浪费，前端用变量保存AJAX请求结果，每次操作本地变量，不用请求，减少请求次数

  （3） 用innerHTML代替DOM操作，减少DOM操作次数，优化javascript性能。

  （4） 当需要设置的样式很多时设置className而不是直接操作style。

  （5） 少用全局变量、缓存DOM节点查找的结果。减少IO读取操作。

  （6） 避免使用CSS Expression（css表达式)又称Dynamic properties(动态属性)。

  （7） 图片预加载，将样式表放在顶部，将脚本放在底部  加上时间戳。

  （8） 避免在页面的主体布局中使用table，table要等其中的内容完全下载之后才会显示出来，显示比div+css布局慢。
  对普通的网站有一个统一的思路，就是尽量向前端优化、减少数据库操作、减少磁盘IO。向前端优化指的是，在不影响功能和体验的情况下，能在浏览器执行的不要在服务端执行，能在缓存服务器上直接返回的不要到应用服务器，程序能直接取得的结果不要到外部取得，本机内能取得的数据不要到远程取，内存能取到的不要到磁盘取，缓存中有的不要去数据库查询。减少数据库操作指减少更新次数、缓存结果减少查询次数、将数据库执行的操作尽可能的让你的程序完成（例如join查询），减少磁盘IO指尽量不使用文件系统作为缓存、减少读写文件次数等。程序优化永远要优化慢的部分，换语言是无法“优化”的。
http状态码有那些？分别代表是什么意思？
    简单版
    [
        100  Continue   继续，一般在发送post请求时，已发送了http header之后服务端将返回此信息，表示确认，之后发送具体参数信息
        200  OK         正常返回信息
        201  Created    请求成功并且服务器创建了新的资源
        202  Accepted   服务器已接受请求，但尚未处理
        301  Moved Permanently  请求的网页已永久移动到新位置。
        302 Found       临时性重定向。
        303 See Other   临时性重定向，且总是使用 GET 请求新的 URI。
        304  Not Modified 自从上次请求后，请求的网页未修改过。

        400 Bad Request  服务器无法理解请求的格式，客户端不应当尝试再次使用相同的内容发起请求。
        401 Unauthorized 请求未授权。
        403 Forbidden   禁止访问。
        404 Not Found   找不到如何与 URI 相匹配的资源。

        500 Internal Server Error  最常见的服务器端错误。
        503 Service Unavailable 服务器端暂时无法处理请求（可能是过载或维护）。
    ]

  完整版
  1**(信息类)：表示接收到请求并且继续处理
    100——客户必须继续发出请求
    101——客户要求服务器根据请求转换HTTP协议版本

  2**(响应成功)：表示动作被成功接收、理解和接受
    200——表明该请求被成功地完成，所请求的资源发送回客户端
    201——提示知道新文件的URL
    202——接受和处理、但处理未完成
    203——返回信息不确定或不完整
    204——请求收到，但返回信息为空
    205——服务器完成了请求，用户代理必须复位当前已经浏览过的文件
    206——服务器已经完成了部分用户的GET请求

  3**(重定向类)：为了完成指定的动作，必须接受进一步处理
    300——请求的资源可在多处得到
    301——本网页被永久性转移到另一个URL
    302——请求的网页被转移到一个新的地址，但客户访问仍继续通过原始URL地址，重定向，新的URL会在response中的Location中返回，浏览器将会使用新的URL发出新的Request。
    303——建议客户访问其他URL或访问方式
    304——自从上次请求后，请求的网页未修改过，服务器返回此响应时，不会返回网页内容，代表上次的文档已经被缓存了，还可以继续使用
    305——请求的资源必须从服务器指定的地址得到
    306——前一版本HTTP中使用的代码，现行版本中不再使用
    307——申明请求的资源临时性删除

  4**(客户端错误类)：请求包含错误语法或不能正确执行
    400——客户端请求有语法错误，不能被服务器所理解
    401——请求未经授权，这个状态代码必须和WWW-Authenticate报头域一起使用
    HTTP 401.1 - 未授权：登录失败
    　　HTTP 401.2 - 未授权：服务器配置问题导致登录失败
    　　HTTP 401.3 - ACL 禁止访问资源
    　　HTTP 401.4 - 未授权：授权被筛选器拒绝
    HTTP 401.5 - 未授权：ISAPI 或 CGI 授权失败
    402——保留有效ChargeTo头响应
    403——禁止访问，服务器收到请求，但是拒绝提供服务
    HTTP 403.1 禁止访问：禁止可执行访问
    　　HTTP 403.2 - 禁止访问：禁止读访问
    　　HTTP 403.3 - 禁止访问：禁止写访问
    　　HTTP 403.4 - 禁止访问：要求 SSL
    　　HTTP 403.5 - 禁止访问：要求 SSL 128
    　　HTTP 403.6 - 禁止访问：IP 地址被拒绝
    　　HTTP 403.7 - 禁止访问：要求客户证书
    　　HTTP 403.8 - 禁止访问：禁止站点访问
    　　HTTP 403.9 - 禁止访问：连接的用户过多
    　　HTTP 403.10 - 禁止访问：配置无效
    　　HTTP 403.11 - 禁止访问：密码更改
    　　HTTP 403.12 - 禁止访问：映射器拒绝访问
    　　HTTP 403.13 - 禁止访问：客户证书已被吊销
    　　HTTP 403.15 - 禁止访问：客户访问许可过多
    　　HTTP 403.16 - 禁止访问：客户证书不可信或者无效
    HTTP 403.17 - 禁止访问：客户证书已经到期或者尚未生效
    404——一个404错误表明可连接服务器，但服务器无法取得所请求的网页，请求资源不存在。eg：输入了错误的URL
    405——用户在Request-Line字段定义的方法不允许
    406——根据用户发送的Accept拖，请求资源不可访问
    407——类似401，用户必须首先在代理服务器上得到授权
    408——客户端没有在用户指定的饿时间内完成请求
    409——对当前资源状态，请求不能完成
    410——服务器上不再有此资源且无进一步的参考地址
    411——服务器拒绝用户定义的Content-Length属性请求
    412——一个或多个请求头字段在当前请求中错误
    413——请求的资源大于服务器允许的大小
    414——请求的资源URL长于服务器允许的长度
    415——请求资源不支持请求项目格式
    416——请求中包含Range请求头字段，在当前请求资源范围内没有range指示值，请求也不包含If-Range请求头字段
    417——服务器不满足请求Expect头字段指定的期望值，如果是代理服务器，可能是下一级服务器不能满足请求长。

  5**(服务端错误类)：服务器不能正确执行一个正确的请求
    HTTP 500 - 服务器遇到错误，无法完成请求
    　　HTTP 500.100 - 内部服务器错误 - ASP 错误
    　　HTTP 500-11 服务器关闭
    　　HTTP 500-12 应用程序重新启动
    　　HTTP 500-13 - 服务器太忙
    　　HTTP 500-14 - 应用程序无效
    　　HTTP 500-15 - 不允许请求 global.asa
    　　Error 501 - 未实现
  HTTP 502 - 网关错误
  HTTP 503：由于超载或停机维护，服务器目前无法使用，一段时间后可能恢复正常
一个页面从输入 URL 到页面加载显示完成，这个过程中都发生了什么？（流程说的越详细越好）
  注：这题胜在区分度高，知识点覆盖广，再不懂的人，也能答出几句，
  而高手可以根据自己擅长的领域自由发挥，从URL规范、HTTP协议、DNS、CDN、数据库查询、
  到浏览器流式解析、CSS规则构建、layout、paint、onload/domready、JS执行、JS API绑定等等；

  详细版：
    1、浏览器会开启一个线程来处理这个请求，对 URL 分析判断如果是 http 协议就按照 Web 方式来处理;
    2、调用浏览器内核中的对应方法，比如 WebView 中的 loadUrl 方法;
    3、通过DNS解析获取网址的IP地址，设置 UA 等信息发出第二个GET请求;
    4、进行HTTP协议会话，客户端发送报头(请求报头);
    5、进入到web服务器上的 Web Server，如 Apache、Tomcat、Node.JS 等服务器;
    6、进入部署好的后端应用，如 PHP、Java、JavaScript、Python 等，找到对应的请求处理;
    7、处理结束回馈报头，此处如果浏览器访问过，缓存上有对应资源，会与服务器最后修改时间对比，一致则返回304;
    8、浏览器开始下载html文档(响应报头，状态码200)，同时使用缓存;
    9、文档树建立，根据标记请求所需指定MIME类型的文件（比如css、js）,同时设置了cookie;
    10、页面开始渲染DOM，JS根据DOM API操作DOM,执行事件绑定等，页面显示完成。

  简洁版：
    浏览器根据请求的URL交给DNS域名解析，找到真实IP，向服务器发起请求；
    服务器交给后台处理完成后返回数据，浏览器接收文件（HTML、JS、CSS、图象等）；
    浏览器对加载到的资源（HTML、JS、CSS等）进行语法解析，建立相应的内部数据结构（如HTML的DOM）；
    载入解析到的资源文件，渲染页面，完成。
部分地区用户反应网站很卡，请问有哪些可能性的原因，以及解决方法？
从打开app到刷新出内容，整个过程中都发生了什么，如果感觉慢，怎么定位问题，怎么解决?
除了前端以外还了解什么其它技术么？你最最厉害的技能是什么？
你用的得心应手用的熟练地编辑器&开发环境是什么样子？
Sublime Text 3 + 相关插件编写前端代码
Google chrome 、Mozilla Firefox浏览器 +firebug 兼容测试和预览页面UI、动画效果和交互功能
Node.js+Gulp
git 用于版本控制和Code Review
对前端工程师这个职位是怎么样理解的？它的前景会怎么样？
前端是最贴近用户的程序员，比后端、数据库、产品经理、运营、安全都近。
1、实现界面交互
2、提升用户体验
3、有了Node.js，前端可以实现服务端的一些事情


前端是最贴近用户的程序员，前端的能力就是能让产品从 90分进化到 100 分，甚至更好，

参与项目，快速高质量完成实现效果图，精确到1px；

与团队成员，UI设计，产品经理的沟通；

做好的页面结构，页面重构和用户体验；

处理hack，兼容、写出优美的代码格式；

针对服务器的优化、拥抱最新前端技术。
你怎么看待Web App 、hybrid App、Native App？
你移动端前端开发的理解？（和 Web 前端开发的主要区别是什么？）
你对加班的看法？
加班就像借钱，原则应当是------救急不救穷
平时如何管理你的项目？
先期团队必须确定好全局样式（globe.css），编码模式(utf-8) 等；

编写习惯必须一致（例如都是采用继承式的写法，单样式都写成一行）；

标注样式编写人，各模块都及时标注（标注关键样式调用的地方）；

页面进行标注（例如 页面 模块 开始和结束）；

CSS跟HTML 分文件夹并行存放，命名都得统一（例如style.css）；

JS 分文件夹存放 命名以该JS功能为准的英文翻译。

图片采用整合的 images.png png8 格式文件使用 尽量整合在一起使用方便将来的管理
如何设计突发大规模并发架构？
当团队人手不足，把功能代码写完已经需要加班的情况下，你会做前端代码的测试吗？
说说最近最流行的一些东西吧？常去哪些网站？
    ES6\WebAssembly\Node\MVVM\Web Components\React\React Native\Webpack 组件化
知道什么是SEO并且怎么优化么? 知道各种meta data的含义么?
移动端（Android IOS）怎么做好用户体验?
清晰的视觉纵线、
信息的分组、极致的减法、
利用选择代替输入、
标签及文字的排布方式、
依靠明文确认密码、
合理的键盘利用
简单描述一下你做过的移动APP项目研发流程？
你在现在的团队处于什么样的角色，起到了什么明显的作用？
你认为怎样才是全端工程师（Full Stack developer）？
介绍一个你最得意的作品吧？
你有自己的技术博客吗，用了哪些技术？
对前端安全有什么看法？
是否了解Web注入攻击，说下原理，最常见的两种攻击（XSS 和 CSRF）了解到什么程度？
项目中遇到国哪些印象深刻的技术难题，具体是什么问题，怎么解决？。
最近在学什么东西？
你的优点是什么？缺点是什么？
如何管理前端团队?
最近在学什么？能谈谈你未来3，5年给自己的规划吗？
转自：@markyun 
原文：https://github.com/markyun/My-blog/tree/master/Front-end-Developer-Questions/Questions-and-Answers
  
  
  [1]: /img/bVldFY
  [2]: http://segmentfault.com/blog/trigkit4/1190000000718840
  [3]: http://segmentfault.com/blog/trigkit4/1190000000660786#articleHeader15
  [4]: http://segmentfault.com/blog/trigkit4/1190000000687844
  [5]: http://segmentfault.com/blog/trigkit4/1190000000758184#articleHeader5
  [6]: http://segmentfault.com/blog/trigkit4/1190000000800711#articleHeader30
  [7]: http://segmentfault.com/blog/trigkit4/1190000000656717
  [8]: http://segmentfault.com/blog/trigkit4/1190000000697254
  [9]: http://segmentfault.com/blog/trigkit4/1190000002440502
  [10]: http://segmentfault.com/blog/trigkit4/1190000000691919
  [11]: http://segmentfault.com/blog/trigkit4/1190000002585760
  [12]: http://segmentfault.com/blog/trigkit4/1190000000652891
  [13]: http://segmentfault.com/blog/trigkit4/1190000002174034
  [14]: http://segmentfault.com/blog/trigkit4/1190000000691919
  [15]: http://segmentfault.com/blog/trigkit4/1190000000733959
